---
name: Intercept | Downgrading Managed Services plan
about: v2023.01
title: "[Downgrading Managed Services plan] %customer%"
labels: ISSUE
assignees: ''

---

### Description

The following steps needs to be done in case of a downgrade from Managed Services to CSP Support.

---
### CSM Tasks 
   - [ ] Customer has send a notice of contract termination
   - [ ] Contract enddate: ""
   - [ ] CSM >> A confirmation of contract termination is sent to the customer
   - [ ] CSM >> A new agreement is send to the customer for CSP Support. 
   - [ ] CSM >> Adjust articals in Reassure
   - [ ] CSM >> Adjust contract in TOPdesk
   

### Technical steps
   - [ ] Engineer >> Remove customer from PRTG
   - [ ] Engineer >> Remove PRTG Probe from there enviroment
   - [ ] Engineer >> Remove all Intercept Resources
   - [ ] Engineer >> Run onboarding scripting again with CSP Support level. This will update Lighthouse


