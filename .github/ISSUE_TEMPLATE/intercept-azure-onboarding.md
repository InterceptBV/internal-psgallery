---
name: Intercept | Azure Onboarding
about: v2022.10
title: "[Azure Onboarding] %customer%"
labels: EPIC
assignees: ''

---

### Description
%generic description of the azure onboarding, what is discussed with customer beforehand% 

Main Project number: `xxx`

SLA Project number: `xxx`

Microsoft Funding: `Yes / No`

Managed Services: `Yes / No`

Deadline: `xxx`

---
### Project Management

- [ ] Project manager has a signed order
- [ ] Project manager made the intake form availible
- [ ] Consultant made a concept version of the `Work Breakdown`[^1]
- [ ] Consultant stored the `Work Breakdown`[^1] in the project folder
- [ ] Consultant converted concept to final version
- [ ] `Work Breakdown`[^1] is send
- [ ] `Work Breakdown`[^1] is agreed by customer
- [ ] Project manager converted `Work Breakdown`[^1] into GitHub issues and connects to this EPIC
- [ ] Project manager has assigned the customer to a GitHub Team board
- [ ] Project manager scheduled a Kick off meeting
- [ ] Project manager shared the project report
- [ ] Project manager scheduled a status sync meeting
- [ ] Project manager closed the project and survey is send to customer

---
### Work Breakdown

- [ ] Example step 1
- [ ] Example step 2

---
### Managed Services

   - [ ] Project manager gives the go-ahead to onboard customer to Managed Services

#### SLA & Pre-checks
   - [ ] Sales receives a signed SLA
   - [ ] Sales has stored the SLA in the `Intercept | SLA Folder`[^6]
   - [ ] CSM has validated that the customer is in the `Intercept | Portal`[^5]
   - [ ] CSM has created the SLA articles in the `Intercept | Portal`[^5]
   - [ ] CSM has validated the configured pricing in the `Intercept | Portal`[^5]
   - [ ] CSM has validated the SLA contract in `TOPdesk`[^2]
   - [ ] CSM has checked relevant customer contact persons in `TOPdesk`[^2]
   - [ ] CSM has checked relevant customer contact persons are tagged on the customer card within `Hubspot`
   - [ ] CSM has validated the SLA contract in `Exact Online`
   - [ ] CSM - Activating CSP customer contract


#### Inventory & Customer meeting
   - [ ] Engineer created a `Managedable Resource Sheet`[^4] & shared in current issue
   - [ ] CSM Planned a `Welcome to Intercept` meeting
   - [ ] Customer has reviewed the `Manageable Resource Sheet`[^4]
   - [ ] CSM shared the results in current issue
   - [ ] CSM Planned a `Managed Service - Kick off` meeting
   - [ ] Cost Management - Set the right budget in Partner Center
   - [ ] Cost Management - Disuss with the customer a budget alert that must be set on subscription level

##### Kick off checklist
   - [ ] CSM has set Customer and Intercept expectations
   - [ ] Customer has met the team of Engineers
   - [ ] Communication charts/flows
   - [ ] Engineer discussed `Managedable Resource Sheet`[^4] with the customer
   - [ ] Engineer discussed back-up schedule & policies with the customer (RPO & RTO)
   - [ ] Engineer discussed pathmanagement with the customer 
   - [ ] Engineer discussed Microsoft Defender for Cloud for all tagged resources

#### Configure & deploy
   - [ ] Engineer has tagged all resources that are marked in in `Managedable Resource Sheet`[^4]
   - [ ] Engineer has reviewed & ensured the Azure Advisor configuration if everything is enabled
   - [ ] Engineer has reviewed & ensured Azure Ligthouse
   - [ ] Engineer has reviewed & ensured Microsoft Defender for cloud is enabled for all tagged resources
   - [ ] Engineer has deployed the `Intercept | Azure Policy`
   - [ ] Engineer determined other credentials necessary to maintain the customer environment & stored it in `Intercept | PasswordState`[^7]
   - [ ] Engineer has deployed & configured back-up (policies) according to the agreed schedule
   - [ ] Engineer has deployed $ configured patchmanagement according to the agreed schedule
   - [ ] Engineer has deployed & configured monitoring & alerting for all tagged resources
   - [ ] Engineer has ensured that the monthly PARC report is set up and planned
   - [ ] Engineer has created documentation
   - [ ] Infrastructure as code changes pushed to customer repo

##### Intercept Portal
   - [ ] Engineer activated the Azure Policy dashboard in the `Intercept | Portal`[^5]
   - [ ] Engineer invited relevent customer contact to the `Intercept | Portal`[^5]

---

### Finalizing
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
