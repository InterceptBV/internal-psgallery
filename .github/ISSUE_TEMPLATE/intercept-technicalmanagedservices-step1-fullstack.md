---
name: Intercept | Technical Onboarding Managed Services - STEP 1 - Full Stack
about: v2023.09
title: "[Technical Managed Services Onboarding STEP 1 Full Stack] %customer%"
labels: EPIC
assignees: ''

---

### Requirements

- [ ] Sales >> TenantID: `xxx`
- [ ] Sales >> Tenant Name: `xxx`
- [ ] Sales >> Subscription ID's: `xxx`
- [ ] Sales >> Email address for technical alerts: `xxx`
- [ ] Sales >> Email address for budget alerts: `xxx`
- [ ] Sales / Engineer >> Export list of Azure Resources
- [ ] Sales / Engineer >> Discuss with customer which Azure resources needs te be managed
- [ ] Project Management >> Project available in Exact Online
- [ ] Project Management >> Customer available in Reassure
- [ ] Project Management >> Customer in TOPdesk, via Reassure function

---

#### STEP A - Check
   - [ ] Engineer >> if needed, reseller request is accepted by customer
   - [ ] Engineer >> authorization Intercept to customer tenant / subscription

#### STEP B - Run script 1
   - [ ] Engineer >> Run Script 1 >> New-InterceptOnboarding.ps1
(Scipt is responsible for: authorize as admin/owner + app registration + deploy Lighthouse + Defender for Cloud + Cost Mgmt with alerts + Intercept policies)

#### STEP C - Manual
   - [ ] Engineer >> Tag all managed resources

#### STEP D - Run script 2
   - [ ] Engineer >> Enable Monitoring and Alerting
---
