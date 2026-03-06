---
description: 'Infrastructure as Code with Bicep'
applyTo: '**/*.{bicep,bicepparam}'
---

# GitHub Copilot Instructions for Bicep Development

These instructions apply to all `.bicep` and `.bicepparam` files in this repository.

## Overview

This repository contains Bicep infrastructure-as-code following Intercept's coding standards. When generating or modifying Bicep code, always adhere to these standards for consistency, maintainability, and best practices.

## Naming Conventions

Follow Azure CAF naming convention: `resourceAbbreviation-projectName-environment-shortenedLocation`

**Components:**
- `resourceAbbreviation`: Azure CAF abbreviation (e.g., `rg`, `vnet`, `kv`, `st`, `aks`)
- `projectName`: Short project or customer name (e.g., `customer`, `project`)
- `environment`: `dev`, `test`, `acc`, or `prod`
- `shortenedLocation`: `weu` (West Europe), `neu` (North Europe), `uks` (UK South), etc.

**Examples:**
```bicep
param aksResourceGroupName string = 'rg-aks-customer-prod-weu'
param vNetName string = 'vnet-customer-prod-weu'
param keyVaultName string = take('kvcustomerprodweu', 24) // Example without hyphens to conserve length; some resources (e.g., storage accounts) require names without hyphens
```

## File Structure

Structure Bicep files in this order:

1. **Imports** - Type imports from AVM modules
2. **Target Scope** - Deployment scope declaration
3. **Parameters & Variables** - Grouped by resource area with section comments
4. **Existing Resources** - References to existing Azure resources
5. **Modules & Resources** - In dependency order

**Example structure:**
```bicep
// File-level documentation
// This file deploys AKS infrastructure at subscription scope

import { extensionType } from 'br/public:avm/res/container-service/managed-cluster:0.12.0'

targetScope = 'subscription'

/*
// General Parameters
*/
@description('Environment name')
@allowed(['dev', 'test', 'acc', 'prod'])
param environmentName string

/*
// Resource Group parameters
*/
@description('Name of the resource group for AKS')
param aksResourceGroupName string = 'rg-aks-${customerName}-${environmentName}-${locationShortCode}'

var resourceGroupArray = [
  {
    name: aksResourceGroupName
    location: location
  }
]

/*
// Existing Resources
*/
resource existingVNet 'Microsoft.Network/virtualNetworks@2025-01-01' existing = if (useExistingVNet) {
  name: vNetName
  scope: resourceGroup(existingSubscriptionId, existingResourceGroup)
}

/*
// Modules
*/
module resourceGroups 'br/public:avm/res/resources/resource-group:0.4.3' = [
  for (rg, i) in resourceGroupArray: {
    name: 'rg-${i}-deployment'
    params: {
      name: rg.name
      location: rg.location
      tags: tags
    }
  }
]
```

## Azure Verified Modules (AVM)

**ALWAYS use AVM modules from the public registry - NEVER download them locally.**

```bicep
// ✅ Correct - Reference from public registry
module vnet 'br/public:avm/res/network/virtual-network:0.7.2' = {
  name: 'deploy-vnet'
  params: {
    name: vNetName
    location: location
  }
}

// ❌ Incorrect - Downloaded module
module vnet './modules/network/virtual-network/main.bicep' = {
  // Don't do this for AVM modules
}
```

**Custom modules** go in `modules/Custom/` directory only:
```bicep
module customLogic './modules/Custom/specialProcessing/main.bicep' = {
  name: 'custom-processing'
  params: {
    customParam: value
  }
}
```

**Version Pinning:**
- ALWAYS pin to specific module versions: `:{version}`
- Use semantic versioning (e.g., `:0.30.0`)
- Review module changelog before upgrading
- Test version upgrades in non-production environments first

**Module Discovery:**
- Search Bicep public registry: `br/public:avm/res/{service}/{resource}:{version}`
- Browse available modules: [Bicep Registry Modules](https://github.com/Azure/bicep-registry-modules/tree/main/avm/res)
- Review module README and examples before implementation
- Check [AVM Documentation](https://azure.github.io/Azure-Verified-Modules/) for guidance

## Parameters and Variables

**Parameters:**
- Use camelCase naming
- ALWAYS include `@description()` decorator (or `@sys.description()` - both are valid)
- Use `@minLength()` and `@maxLength()` for naming parameters
- Use `@allowed()` decorator **sparingly** - it can block valid deployments when Azure adds new options
- Set default values safe for test environments (use low-cost SKUs)
- Use `@secure()` for sensitive values
- Group related parameters together with section comments
- Place related variables immediately after their parameters

```bicep
@description('Virtual Network Name')
param vNetName string = 'vnet-${customerName}-${environmentName}-${locationShortCode}'

@description('Virtual Network Address Prefix')
param vNetAddressPrefix string = '10.0.0.0/16'

var vNetConfiguration = {
  Subnets: [
    {
      name: aksNodeSubnetName
      addressPrefix: aksNodeSubnetPrefix
    }
  ]
}
```

**Variables:**
- Use camelCase naming
- Place near the parameters they depend on
- Break complex logic into multiple variables for readability
- Use variables for complex expressions instead of embedding them directly in resource properties
- Use `loadJsonContent()` for loading external configuration files

**Example with external config:**
```bicep
var config = loadJsonContent('config.json')
var settings = config.environmentSettings[environmentName]
```

## Symbolic Names and Resource References

**Symbolic Names:**
- Use descriptive symbolic names that represent the resource type (e.g., `storageAccount`, `keyVault`)
- Avoid using 'name' in symbolic names (use `storageAccount` not `storageAccountName`)
- Use camelCase for all symbolic names

**Resource References:**
- Use symbolic names for resource references instead of `reference()` or `resourceId()` functions
- Create resource dependencies through symbolic names (e.g., `storageAccount.id`) not explicit `dependsOn`
- For accessing properties from other resources, use the `existing` keyword instead of passing values through outputs

```bicep
// ✅ Good - Using symbolic name reference
resource storageAccount 'Microsoft.Storage/storageAccounts@2023-01-01' = {
  name: storageAccountName
  location: location
  // ...
}

resource functionApp 'Microsoft.Web/sites@2023-01-01' = {
  name: functionAppName
  location: location
  properties: {
    serverFarmId: appServicePlan.id // Implicit dependency through symbolic name
  }
}

// ✅ Good - Using existing keyword
resource existingVNet 'Microsoft.Network/virtualNetworks@2025-01-01' existing = {
  name: vNetName
  scope: resourceGroup(existingSubscriptionId, existingResourceGroup)
}

var subnetId = existingVNet.properties.subnets[0].id

// ❌ Bad - Using reference() function
output storageAccountId string = reference(storageAccountName).id

// ❌ Bad - Using resourceId() unnecessarily
var storageId = resourceId('Microsoft.Storage/storageAccounts', storageAccountName)
```

## Types

**Import types from AVM modules when available:**
```bicep
import { extensionType } from 'br/public:avm/res/container-service/managed-cluster:0.12.0'
import { agentPoolType } from 'br/public:avm/res/container-service/managed-cluster:0.12.0'
```

**Use user-defined types for complex parameter structures:**
```bicep
type subnetConfig = {
  name: string
  addressPrefix: string
  @description('Optional network security group resource ID')
  networkSecurityGroupResourceId: string?
}

param subnets subnetConfig[]
```

**Benefits:**
- Strong typing prevents configuration errors
- IntelliSense support in VS Code
- Reusable type definitions
- Self-documenting parameter structures

## Comments

**Use comments sparingly** - prefer self-documenting code with descriptive names and `@description()` decorators.

**When to use comments:**

✅ **Section headers** to organize the file:
```bicep
/*
// Virtual Networking parameters
*/
```

✅ **File-level documentation** at the top:
```bicep
// This file operates at subscription level
// Deploys AKS infrastructure with networking and monitoring
```

✅ **Brief clarifications** when necessary:
```bicep
// Helper variables to calculate subnet indices
var nodeSubnetIndex = 0
```

**When NOT to use comments:**

❌ Explaining obvious code  
❌ Restating what `@description()` already says  
❌ Long explanations (refactor the code instead)  
❌ Commented-out code (remove it)  

```bicep
// ❌ Bad - Obvious and redundant
// Set the location to West Europe
param location string = 'westeurope'

// ✅ Good - Use @description instead of comments
@description('Azure region for resource deployment')
param location string = 'westeurope'
```

## Subnet Naming

**Custom subnets** use `snet-` prefix with descriptive names:
- `snet-aks-nodes`
- `snet-aks-pods`
- `snet-management`
- `snet-private-endpoints`
- `snet-application`

**Azure-required subnet names** (must be exact):
- `GatewaySubnet`
- `AzureFirewallSubnet`
- `AzureBastionSubnet`
- `AzureFirewallManagementSubnet`

## Security Best Practices

- Use `@secure()` decorator for sensitive parameters
- Never hardcode secrets or credentials
- **Never include secrets or keys in outputs** - outputs are logged and visible
- Use managed identities where possible (prefer system-assigned)
- Configure private endpoints for PaaS services when required
- Apply tags consistently across all resources
- Use Key Vault for secrets management
- Use resource properties directly in outputs (e.g., `storageAccount.properties.primaryEndpoints`)

```bicep
@secure()
@description('Admin password for the virtual machine')
param adminPassword string

// ✅ Use managed identity
managedIdentities: {
  systemAssigned: true
}

// ✅ Apply consistent tags
param tags object = {
  Environment: environmentName
  Customer: customerName
  LastUpdatedOn: utcNow('dd/MM/yyyy')
}

// ❌ Bad - Never output secrets
output storageAccountKey string = storageAccount.listKeys().keys[0].value

// ✅ Good - Output safe properties only
output storageAccountName string = storageAccount.name
output blobEndpoint string = storageAccount.properties.primaryEndpoints.blob
```

## Deployment Order

Deploy modules in logical dependency order:

1. Resource Groups
2. Networking (VNets, Subnets, NSGs, Route Tables)
3. Identity (Managed Identities)
4. Core Infrastructure (Key Vault, Container Registry)
5. Dependent Services (AKS, App Services, Databases)

Use `dependsOn` only when dependencies aren't implicit:
```bicep
module vnet 'br/public:avm/res/network/virtual-network:0.7.2' = {
  scope: resourceGroup(resourceGroupName)
  name: 'deploy-vnet'
  params: {
    name: vNetName
    location: location
  }
  dependsOn: [resourceGroups] // Only if not implicit from scope
}
```

## Code Quality

- Use camelCase for all parameter and variable names
- Keep files organized and readable
- Break large files into smaller modules (avoid files >1000 lines)
- Use string interpolation: `'rg-${customerName}-${environmentName}'`
- Use ternary operators for simple conditions: `condition ? trueValue : falseValue`
- Use array operations: `union()`, `filter()`, `map()`
- No magic numbers - use parameters or named variables
- **Use latest stable API versions** for all resources
- Specify minimum and maximum character length for naming parameters using `@minLength()` and `@maxLength()`

## Common Patterns

**Resource loops:**
```bicep
module resourceGroups 'br/public:avm/res/resources/resource-group:0.4.3' = [
  for (rg, i) in resourceGroupArray: {
    name: 'rg-${i}-deployment'
    params: {
      name: rg.name
      location: rg.location
    }
  }
]
```

**Controlling loop parallelism with `@batchSize()`:**

By default Bicep deploys loop iterations in parallel. Use `@batchSize()` to limit concurrency when resources have ordering constraints or to avoid API throttling:
```bicep
@batchSize(2)
module storageAccounts 'br/public:avm/res/storage/storage-account:0.14.3' = [
  for (account, i) in storageAccountArray: {
    name: 'storage-${i}-deployment'
    params: {
      name: account.name
      location: location
    }
  }
]
```

**Conditional deployment:**
```bicep
module bastion 'br/public:avm/res/network/bastion-host:0.6.1' = if (bastionEnabled) {
  name: 'deploy-bastion'
  params: {
    name: bastionName
    location: location
  }
}
```

**Existing resource reference:**
```bicep
resource existingVNet 'Microsoft.Network/virtualNetworks@2025-01-01' existing = if (useExistingVNet) {
  name: vNetName
  scope: resourceGroup(existingSubscriptionId, existingResourceGroup)
}
```

**Unique resource names:**
```bicep
// Use uniqueString() for globally unique names
var uniqueSuffix = uniqueString(resourceGroup().id, deployment().name)
// Storage account names: 3-24 chars, lowercase alphanumeric only
var storageAccountName = take('st${toLower(customerName)}${uniqueSuffix}', 24)

// Key Vault names: 3-24 chars, alphanumeric and hyphens (no trailing hyphens)
// Avoid hyphens near the take() boundary to prevent invalid trailing-hyphen names
var keyVaultName = take('kv${customerName}${uniqueString(resourceGroup().id)}', 24)
```

**Child resources:**
```bicep
// ✅ Good - Using parent property
resource storageAccount 'Microsoft.Storage/storageAccounts@2023-01-01' = {
  name: storageAccountName
  location: location
}

resource blobService 'Microsoft.Storage/storageAccounts/blobServices@2023-01-01' = {
  parent: storageAccount
  name: 'default'
}

// ❌ Bad - Excessive nesting
resource storageAccount 'Microsoft.Storage/storageAccounts@2023-01-01' = {
  name: storageAccountName
  resource blobService 'blobServices' = {
    name: 'default'
    resource container 'containers' = {
      name: 'data'
      resource immutability 'immutabilityPolicies' = {
        // Too deeply nested - hard to read
      }
    }
  }
}
```

## Build Validation

**MANDATORY: Always validate Bicep files after changes**

```powershell
# Ensure Bicep CLI is up to date
az bicep upgrade

# Lint Bicep files for best practice violations
az bicep lint --file main.bicep

# Build and validate changed Bicep files
az bicep build --file main.bicep
```

**Bicep Parameter Files (.bicepparam):**
- ALWAYS update accompanying `*.bicepparam` files when modifying `*.bicep` files
- Validate parameter files match current parameter definitions
- Test deployments with parameter files before committing

**Example parameter file:**
```bicep
using './main.bicep'

param customerName = 'contoso'
param environmentName = 'prod'
param location = 'westeurope'
```

## What NOT to Do

❌ Download AVM modules into the repository  
❌ Edit AVM modules directly  
❌ Use non-standard naming conventions  
❌ Hardcode values that should be parameters  
❌ Skip `@description()` decorators  
❌ Over-comment obvious code  
❌ Create monolithic files instead of using modules  
❌ Ignore security best practices  
❌ Use outdated API versions from internet examples  
❌ Use `reference()` or `resourceId()` functions when symbolic names work  
❌ Include secrets or keys in outputs  
❌ Excessively nest child resources  
❌ Use `@allowed()` too broadly (blocks future Azure options)  
❌ Forget to update `.bicepparam` files when changing parameters  
❌ Skip `az bicep lint` and `az bicep build` validation before committing  

## References

For complete standards documentation, see:
- [Bicep Standards](https://github.com/InterceptBV/internal-bicep-standards/blob/main/docs/content/docs/bicep-standards.md)
- [Bicep PR Review Guide](https://github.com/InterceptBV/internal-bicep-standards/blob/main/docs/content/docs/bicep-pr-review.md)

## Questions

Contact the Bicep standards team:
- Wilrico Feenstra
- Wesley Haakman
- Richard Hooper
