---
name: Intercept | Onboarding Managed Services
about: v2022.01
title: "[Managed Services Onboarding] %customer%"
labels: EPIC
assignees: ''

---

### Description

- TenantID: `xxx`
- Tenant Name: `xxx`
- Subscription ID's: `xxx`
- Managed Services: CSP, Premium or Full Stack: `xxx`
- Name of the person who did the work: `xxx`
- SLA Project number: `xxx`

---
### Stage 0
   - [ ] CSM >> Sales received a signed SLA
   - [ ] Engineer >> Intercept is authorized as admin/owner to the customer environment

### Stage 1
   - [ ] Engineer >> Create app registration in customer environment
   - [ ] Engineer >> Tag all managed resources
   - [ ] Engineer >> Enable Monitoring and Alerting
   - [ ] CSM >> Enable customer portal access
   - [ ] CSM >> Start invoice run via Exact Online

### Stage 2
   - [ ] CSM >> Planned a `Welcome to Intercept` meeting
   - [ ] CSM >> Communication chart/flow
   - [ ] CSM >> invited relevent customer contact to the `Intercept | Portal`[^5]
   - [ ] CSM >> Created the SLA articles in the `Intercept | Portal`[^5]
   - [ ] CSM >> Validate the configured pricing in the `Intercept | Portal`[^5]
   - [ ] CSM >> Validate the SLA contract in `TOPdesk`[^2]
   - [ ] CSM >> Check relevant customer contact persons in `TOPdesk`[^2]
   - [ ] CSM >> Check relevant customer contact persons are tagged on the customer card within `Hubspot`
   - [ ] CSM >> Activate CSP customer contract
   - [ ] CSM >> provide the right budget for in Partner Center, needs to be sent to Rinie or Marc
   - [ ] CSM >> Disuss with the customer a budget alert that must be set on subscription level
   
### Stage 3
   - [ ] Engineer >> Discuss back-up schedule & policies with the customer (RPO & RTO)
   - [ ] Engineer >> Discuss pathmanagement with the customer 
   - [ ] Engineer >> Discuss Microsoft Defender for Cloud for all tagged resources
   - [ ] Engineer >> Tag all resources that are marked in in `Managedable Resource Sheet`[^4]
   - [ ] Engineer >> Review & ensure the Azure Advisor configuration if everything is enabled
   - [ ] Engineer >> Review & ensure Azure Ligthouse
   - [ ] Engineer >> Review & ensure Microsoft Defender for cloud is enabled for all tagged resource
   - [ ] Engineer >> Deployed the `Intercept | Azure Policy`
   - [ ] Engineer >> Determine other credentials necessary to maintain the customer environment & stored it in `Intercept | PasswordState`[^7]
   - [ ] Engineer >> Deployed & configured back-up (policies) according to the agreed schedule
   - [ ] Engineer >> Deployed $ configured patchmanagement according to the agreed schedule
   - [ ] Engineer >> Ensure that the monthly PARC report is set up and planned
   - [ ] Engineer >> Create documentation
   - [ ] Engineer >> Infrastructure as code changes pushed to customer repo
   - [ ] Engineer >> Activated the Azure Policy dashboard in the `Intercept | Portal`[^5]

### Stage 4
   - [ ] CSM checked if relevant customer contact persons are invited
   - [ ] CSM checked if customer have access to the `Intercept | Portal`[^5]
   - [ ] CSM checked if customer have insight within the Intercept SLA report
   - [ ] CSM checked if customer have insight within Azure Policy dashboard
   - [ ] CSM checked if customer have insight within Azure Advisor
   - [ ] CSM checked if customer have access to edit they O365 licenses
   - [ ] CSM checked first invoice and checked if everything is okay

---
[^1]: [Work breakdown | word template](https://interceptbv.sharepoint.com/:w:/g/huisstijl/EWrkRNRL6NFKt8LQFZ4yRwQBDo-Hiz7fhIHOzKA3uXhdKg?e=gf2gaV)
[^2]: [TOPdesk](https://intercept.topdesk.net)
[^4]: [Manageable Resource Sheet](https://github.com/InterceptBV/ms-generic-scripts/blob/main/Script-GenerateManagebleResourcesList/GenerateResourceListExcel.ps1)
[^5]: [Intercept | Portal](https://management.intercept.cloud/)
[^6]: [Intercept | SLA Folder](https://interceptbv.sharepoint.com/:f:/g/intercept/EgpCUNw-g7hPrFyWBE9hWJkBzXRjo0Nc8uC3oBusLeufCw)
[^7]: [Intercept | PasswordState](https://pws.intercept.nl)
