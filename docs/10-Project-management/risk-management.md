# Risk List

## Project Risks

This document outlines potential risks associated with the ECSP1 eCommerce Server Platform project and provides measures to mitigate and address them effectively.


### Project Risk Table

| Risk ID | Name                             | Description                                                                 | Impact | Probability | Mitigation Plan                                                                 | Responsible         |
|---------|----------------------------------|-----------------------------------------------------------------------------|--------|-------------|----------------------------------------------------------------------------------|----------------------|
| RIS001  | Project Scale Creep              | Project expands beyond original scope, causing delays and budget overruns  | S2     | Medium      | Strict scope management and regular backlog review                              | Team Lead            |
| RIS002  | Lack of Resources                | Missing necessary skills, knowledge or personnel                            | S2     | Medium      | Skills audit, proactive training, realistic task allocation                     | Team Lead            |
| RIS003  | Team Member Illness              | A key contributor becomes unavailable                                       | S3     | Medium      | Cross-training and task redundancy                                              | Team Lead            |
| RIS004  | Communication Issues             | Misunderstandings, delays or poor info flow                                 | S2     | High        | Set communication routines (dailies, retros), central documentation             | Team Lead            |
| RIS005  | Schedule Slippage                | Tasks take longer than estimated                                            | S2     | High        | Use time buffers, monitor burndown, escalate early                              | Team Lead            |
| RIS006  | Unclear Goals & Vision           | Team doesn't fully understand the product or scope                          | S2     | Medium      | Define goals clearly in planning documents and reviews                          | Product Owner        |
| RIS007  | Lack of Motivation               | Team disengaged, reducing productivity                                      | S3     | Medium      | Regular feedback, involvement, recognition                                      | Team Lead            |
| RIS008  | Inadequate Documentation         | Missing or outdated technical/process documentation                         | S3     | Medium      | Assign clear documentation tasks, maintain version control                      | Developer / All      |
| RIS009  | Work Overlap                     | Multiple members working on same items unknowingly                          | S3     | Medium      | Use issue boards with assignments and ownership                                 | Developer            |
| RIS010  | Unclear Responsibilities         | Tasks not clearly assigned                                                  | S3     | Medium      | Use RACI model or similar for role clarity                                      | Team Lead            |
| RIS011  | Member Loss                      | A team member leaves the project                                            | S2     | Low         | Ensure handovers, backup resources, documentation                               | Team Lead            |
| RIS012  | Data Breach                      | Unauthorized access to sensitive data                                       | S1     | Low         | Enforce access controls, monitor logs, update security patches                  | Security / Admin     |
| RIS013  | LabraNet Shutdown                | Network environment used by team becomes unavailable                        | S2     | Low         | Backup and prepare fallback network (e.g. local)                                | Admin                |
| RIS014  | Server Configuration Issues      | Misconfigured servers cause deployment or runtime problems                  | S2     | Medium      | Automate deployment via scripts, test in staging                                | Ops / Admin          |
| RIS015  | CSC Pouta Misconfiguration       | VM setup fails or lacks sufficient resources                                | S2     | Medium      | Validate specs before provisioning, monitor resource use                        | Admin                |
| RIS016  | CI/CD Pipeline Failures          | Build/deploy automation breaks                                              | S2     | Medium      | Use fallback deploy methods, test pipeline updates incrementally                | Developer / Admin    |
| RIS017  | Web Security Risks               | Open ports, missing HTTPS, weak authentication                              | S1     | Medium      | Harden services, restrict firewall, use secrets management                      | Security / Admin     |
| RIS018  | Deployment Failure               | Software fails to start or function after deployment                        | S2     | Medium      | Use rollback scripts, test thoroughly before production push                    | DevOps / Admin       |
| RIS019  | Credential Loss                  | Passwords, keys, or secrets are lost or leaked                              | S1     | Low         | Use secret managers, rotate credentials, 2FA                                    | Security             |
| RIS020  | Hardware Issues (Team Devices)   | Developer or tester device breaks or becomes unusable                       | S3     | Medium      | Use cloud dev environments, backup configs                                      | Developer / Team Lead|
| RIS021  | Dependency Vulnerability         | 3rd party libraries have known security flaws                               | S1     | Medium      | Regular dependency scans, use Dependabot or similar tools                       | Developer / Security |
| RIS022  | Version Control Conflicts        | Merge conflicts in Git slow down development                                | S3     | Medium      | Encourage small, frequent commits and code reviews                              | Developer            |
| RIS023  | Insufficient Test Coverage       | Lack of automated tests causes undetected bugs                              | S2     | Medium      | Maintain minimum coverage %, write tests for critical logic                     | Developer            |
| RIS024  | Environment Mismatch             | Local vs production config causes unexpected bugs                           | S2     | Low         | Use containerized environments (e.g., Docker), config standardization           | Developer / Admin    |
| RIS025  | Slow Build Times                 | Large codebase or inefficient tooling delays feedback loop                  | S3     | Medium      | Optimize build steps, use caching, parallel builds                              | Developer            |



### Risk Severity (Impact) Levels

| Severity Class | Description                            | Impact                             |
|----------------|----------------------------------------|-------------------------------------|
| S1             | Force Major – Critical system failure  | Immediate and total disruption of the project; requiring urgent resolution |
| S2             | High Severity – Major functional impact | Significant delays or major disruption; temporary workarounds may exist      |
| S3             | Moderate Impact – Manageable risks     | Noticeable impact on operations; manageable with effort   |
| S4             | Low Severity – Minor issue             | Limited or negligible effect on workflow                  |
| S5             | Observational – No immediate effect     | No current impact; potential future concern           |


### Risk Probability Levels

| Likelihood Level | Description                                                | Example Indicators                                                    |
|------------------|------------------------------------------------------------|-----------------------------------------------------------------------|
| **High**         | Risk is likely to occur during the project unless mitigated | - Similar issue has occurred in previous sprints or projects          |
|                  |                                                            | - Dependencies are known to be unstable or prone to failure           |
|                  |                                                            | - Risk factors already present (e.g., known configuration bugs)       |
| **Medium**       | Risk may occur if not actively monitored or controlled     | - Occasional issues observed in similar environments                  |
|                  |                                                            | - Human error or miscommunication could realistically trigger it      |
|                  |                                                            | - Some uncertainty remains in requirements or external services       |
| **Low**          | Risk is unlikely, but possible under rare conditions       | - Has not occurred before, but cannot be ruled out                    |
|                  |                                                            | - Well-documented and controlled area of the project                  |
|                  |                                                            | - Preventative measures already in place and regularly tested         |


### Action Plan for Risk Occurrence

1. **Identify & Assess**: When a risk materializes, assess its impact and severity.
2. **Immediate Response**: Take pre-planned countermeasures or escalate to the appropriate team members.
3. **Communication**: Inform stakeholders, team members, and other relevant parties.
4. **Documentation**: Record the incident, response taken, and improvements needed for future prevention.
5. **Review & Adjust**: Update the risk management plan based on lessons learned.
