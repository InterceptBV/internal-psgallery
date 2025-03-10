---
name: Intercept | Pre Sales
about: v2022.01
title: "[Pre Sales] %customer%"
labels: EPIC
assignees: ''

---

### Required documents & information
[Hutspot | Procedure](https://interceptbv.sharepoint.com/:w:/g/huisstijl/EWrkRNRL6NFKt8LQFZ4yRwQBDo-Hiz7fhIHOzKA3uXhdKg?e=gf2gaV)

[TOPdesk](https://intercept.topdesk.net)

[Work breakdown | word template](https://interceptbv.sharepoint.com/:w:/g/huisstijl/EWrkRNRL6NFKt8LQFZ4yRwQBDo-Hiz7fhIHOzKA3uXhdKg?e=gf2gaV)

[Managedable Resource Sheet](https://github.com/InterceptBV/ms-generic-scripts/blob/main/Script-GenerateManagebleResourcesList/GenerateResourceListExcel.ps1)

[Intercept | Portal](https://management.intercept.cloud/)

[Intercept | SLA Folder](https://interceptbv.sharepoint.com/:f:/g/intercept/EgpCUNw-g7hPrFyWBE9hWJkBzXRjo0Nc8uC3oBusLeufCw)

[Intercept | PasswordState](https://pws.intercept.nl)



### Description
%generic description of the azure onboarding, what is discussed with customer beforehand% 

Main Project number: `xxx`
Onboarding Project number: `xxx`

Microsoft Funding: `Yes / No`

Managed Services: `Yes / No`

Deadline: `xxx`

---
### Project Management tasks

- [ ] Signed order 
- [ ] Intake form 
- [ ] Work breakdown 
- [ ] Assign to DevOps team 
- [ ] Kick off 
- [ ] Project report 
- [ ] Project status sync meeting 
- [ ] Project closing 
- [ ] Shared design in `Intercept | Customer folder`

---
### Work Breakdown

- [ ] Work Breakdown is completed and agreed by customer

---
### Managed Services

#### SLA & Pre-checks
   - [ ] Sales receives a signed SLA
   - [ ] Sales has stored the SLA in the `Intercept | SLA Folder`
   - [ ] CSM has validated that the customer is in the `Intercept | Portal`
   - [ ] CSM has created the SLA articles in the `Intercept | Portal`
   - [ ] CSM has validated the configured pricing in the `Intercept | Portal`
   - [ ] CSM has validated the SLA contract in `TOPdesk`
   - [ ] CSM has checked relevant customer contact persons in `TOPdesk`
   - [ ] CSM has checked relevant customer contact persons are tagged on the customer card within `Hutspot`
   - [ ] CSM has validated the SLA contract in `Exact-online`


#### Inventory & Customer meeting
   - [ ] Engineer created a `Managedable Resource Sheet` & shared in current issue 
   - [ ] CSM Planned a `Welcome to Intercept` meeting
   - [ ] Customer has reviewed the `Managedable Resource Sheet`
   - [ ] CSM shared the results in current issue
   - [ ] CSM Planned a `Managed Service - Kick off` meeting

##### Kick off checklist
   - [ ] CSM has set Customer and Intercept expectations
   - [ ] Customer has met the team of Engineers
   - [ ] Communication charts/flows
   - [ ] Engineer discussed `Managedable Resource Sheet` with the customer
   - [ ] Engineer discussed back-up schedule & policies with the customer (RPO & RTO)
   - [ ] Engineer discussed pathmanagement with the customer 
   - [ ] Engineer discussed Microsoft Defender for Cloud for all tagged resources

#### Configure & deploy
   - [ ] Engineer has tagged all resources that are marked in in `Managedable Resource Sheet`
   - [ ] Engineer has reviewed & ensured the Azure Advisor configuration if everything is enabled
   - [ ] Engineer has reviewed & ensured Azure ligthouse
   - [ ] Engineer has reviewed & ensured Microsoft Defender for cloud is enabled for all tagged resources
   - [ ] Engineer has deployed the `Intercept | Azure Policy`
   - [ ] Engineer determined other credentials necessary to maintain the customer environment & stored it in `Intercept | PasswordState`
   - [ ] Engineer has deployed & configured back-up (policies) according to the agreed schedule
   - [ ] Engineer has deployed $ configured patchmanagement according to the agreed schedule

   - [ ] Engineer has deployed & configured monitoring & alerting for all tagged resources
   - [ ] Engineer has ensured that the monthly PARC report is set up and planned
   - [ ] Engineer has wirten documentation together with Consultant 

##### Intercept Portal
   - [ ] Engineer activated the Azure Policy dashboard in the `Intercept | Portal`
   - [ ] Engineer invited relevent customer contact to the `Intercept | Portal`

---

### Finalizing
   - [ ] CSM checked if relevant customer contact persons are invited
   - [ ] CSM checked if customer have access to the `Intercept | Portal`
   - [ ] CSM checked if customer have insight within the Intercept SLA report
   - [ ] CSM checked if customer have insight within Azure Policy dashboard
   - [ ] CSM checked if customer have insight within Azure Advisor
   - [ ] CSM checked if customer have access to edit they O365 licenses

   - [ ] CSM checked first invoice and checked if everything is okay

---
