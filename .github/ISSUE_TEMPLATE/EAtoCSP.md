---
name: EA to CSP template
about: Template to create an epic for EA to CSP migration
title: "[EA to CSP] "
labels: epic
assignees: ''

---

# EA to CSP Migration 

## Introduction:
This template is basically setup to support the process regarding the EA to CSP migrations. You can find more details regarding the background and lessons learned of this template by clicking the following [link](https://interceptbv.sharepoint.com/:w:/g/intercept/EdURyurgLxRMuFJHO3eNPdwBy3QS2nLKF5WCXko73yufMw?e=LSX1ch).

## Preparation: 

### Questions upfront
- [ ] Kind of EA contract
- [ ] Currency 
- [ ] Permissions for CSP (GDAP)
- [ ] Quota's 
- [ ] EA Billing Admin
- [ ] Tenant name and ID
- [ ] Marketplace items in EA

### Short introduction meeting
A short meeting with the customer is really important. This way the customer can understand the procedure. The questions above can de discussed and clarified.

## Migration
- [ ] Reseller request
To get started a Reseller Request needs to be approved by a Global Admin on the customer side. This will pop up the customer in Partner Center and is required to get the subscriptions migrated. This step is required before we can proceed with the next steps. The Reseller Request that can be sent out to the customer is listed below:
https://admin.microsoft.com/Adminportal/Home?invType=ResellerRelationship&partnerId=4b1f17f7-26f6-4624-a58c-2bc917bae8f3&msppId=0#/partners/invitation

- [ ] Creating an Azure Plan:
   - Login to Partner Center
   - Select the customer
   - In the ‘subscription’ menu, click on [New Subscription]
   - Click ‘Azure’ and under ‘Type’, select ‘Microsoft Azure’
   - Select ‘Azure Plan’ and click ‘Add to cart’
   - Click ‘Review’
   - Click ‘Buy’ to create an Azure Plan. This will also create an empty subscription
   -
- [ ] Enable Cost Management:
   - Login to the Intercept Portal (https://portal.azure.com/intercept.cloud) 
   - Browse to ‘Cost Management + Billing’
   - Under ‘Billing’, select ‘Customers’
   - Select the customer
   - Under ‘Cost Management’ click ‘Cost Analysis’
   - Click ‘Configure Customer Account’
   - Under 'Cost Management’ click ‘Edit’
   - Select ‘Yes’ and click ‘Save’
   
- [ ] Send Transfer Request:
   - Login to the Intercept Portal (https://portal.azure.com/intercept.cloud) 
   - Browse to ‘Cost Management + Billing’
   - Under ‘Billing’, select ‘Customers’
   - Select the customer
   - Under ‘Settings’ click ‘Transfer Requests’
   - Click ‘Add a new request’
   - Fill in the EA Billing Admin Account and click ‘Send transfer request’
   - If the EA Billing Admin has no email box attached, click ‘refresh’ and open the request. You can copy and send the link to the customer

- [ ] Check subscriptions
- [ ] Add Foreign Principal for PEC / Support

## Finalizing

After the migration the customer will reside for about 2 months into Intercept CSP. After this period the new CSP will send out a Transfer Request to handover the subscriptions of the customer.

Some things we need to deliver to the new CSP so they can send out the Transfer Request:
-	CSP Name: Intercept B.V.
-	CSP Microsoft ID: 4b1f17f7-26f6-4624-a58c-2bc917bae8f3

The customer is responsible for removing the foreign principal after migration.
