# Offer

|  |  |
|:-:|:-:|
| Document | Offer |
| Author: | Joni Nisula (Team Leader) |
| Version: | v1.0 |
| Date: | 14.6.2025 |

## 1. Object of the tender and procurement situation

<!-- This section is good -->

The "ECSP1 - eCommerce Server Platform V1.0" solution / service to be implemented in this case means an entity comprising the following functionalities:

### EPIC02: Service deployment
  * FEA005: Automate build,test, and deployment processes
  * FEA004: Implement CI/CD pipelines for all services
### EPIC03: Prestashop as service
  * FEA006: Provide managed hosting for PrestaShop instances
  * FEA007 Dockerized Service Production
  * FEA008 Secure Service Access
  * FEA078 Server management
  * FEA009 Provide API access for developers to integrate with other services
### EPIC04: Log management
  * FEA010 Provide real-time log monitoring and analysis capabilities
### EPIC05: Security Enhancements
  * FEA017 Implement security contexts (e.g., run as non-root user) to enhance container security
  * FEA015 Implement PrestaScan Security to scan PrestaShop website
  * FEA016 Set up the security modules
  * FEA020 Database security hardening
### EPIC06: Test Automation
  * FEA022 Acceptance Test Automation
  * FEA023 Integrate test automation into the CI/CD pipeline
### EPIC07: Bug fixes
  * FEA028 Ensure efficient bug reporting and triage processes
  * FEA029 Utilize error tracking tools to proactively identify and address issues
  * FEA030 Integrate with version control systems (e.g., Git)
  * FEA031 Assign bugs to developers and track progress towards resolution
### EPIC08: Registration and login
  * FEA035 Secure user login
  * FEA036 Password recovery
### EPIC09: Service Backup
  * FEA039 Automated Database Backup. Implement automated scheduling for regular database backups
  * FEA040 Implement automated backups of the entire PrestaShop installation, including files, images, and themes
### EPIC10: Performance Tuning
  * FEA045 Page Caching: Implement efficient page caching mechanisms
### EPIC12: Customer Feedback
  * FEA052 General Feedback Forms
### EPIC15:Documentation and training
  * FEA062 General documentation
  * FEA071 Implement and maintain data privacy policies and procedures in compliance with relevant regulations
  * FEA073 Clear crisis communication guidelines and practices
  * FEA074 A Risk Management Checklist for Prestashop

A more detailed description can be found in [requirements specification](https://core-e28f4a.pages.labranet.jamk.fi/20-Requirement-management/requirement-specification/)

## 2. Objectives, requirements and proposed solutions

Our objective is to deliver a robust, scalable, and secure platform that meets modern e-commerce demands. We have identified the following core areas:

**Service deployment**: We want to deploy a service that makes it possible to maintain a secure and reliable operating environment for all users.

**Security**: We want to minimize the risk of data breaches and unauthorized acces to sensitive information.

**Service deployment**: We want to deploy a service that makes it possible to maintain a secure and reliable operating environment for all users.

**PrestaShop as a service**: We want to deliver such a service that is easy to integrate to needs of businesses. We want the service to run smoothly with minimal down time.

**Test Automation**: We want to deliver integrate tesing into CI/CD pipeline. We aim to generate clear and consice test reports, and ensure that comprehensive testing for all interfaces will be done properly

**Business intelligence**: We want to deliver business analytic tools that help business owners to maintain their business.
<!--
* **Security**: We want to minimize the risk of data breaches and unauthorized acces to sensitive information.

* **Service deployment**: We want to deploy a service that makes it possible to maintain a secure and reliable operating environment for all users.

* **PrestaShop as a service**: We want to deliver such a service that is easy to integrate to needs of businesses. We want the service to run smoothly with minimal down time.

* **Test Automation**: We want to deliver integrate tesing into CI/CD pipeline. We aim to generate clear and consice test reports, and ensure that comprehensive testing for all interfaces will be done properly

* **Business intelligence**: We want to deliver business analytic tools that help business owners to maintain their business.
-->

## 3. Delivery and release plan

Below is a high-level schedule to guide our development and release milestones:

* [G1]() Project Agreement Signing: 19.06.2025
* [G2]() Final Testing Plan Completion: 25.07.2025
* [G3]() Trial Operation Launch: 15.08.2025
* [G4]() Production Release: 29.08.2025

We will use an Agile Scrumban approach to manage development and ensure continuous feedback loops.

### Steps:

* **G1** Plan presentation and Offer proposal 19.06.2025
* **G2** Implementation and testing status check 25.7.2025
* **G3** Demo for the first beta-version 15.8.2025
* **G4** Delivery day 29.08.2025

## 4. Prices and charges

Total feature price **85 293,88 €** (incl. 15% profit margrin + VAT 25,5%)

### Feature Prices

| EPIC                         | Feature Description                                                                                   | In Plan | Priority | Familiarization | Design | Implementation | Testing | Documentation | Deployment | Total Hours | Total Work Price | With 15% Profit | With 25.5% VAT |
|-----------------------------|--------------------------------------------------------------------------------------------------------|---------|----------|------------------|--------|------------------|---------|----------------|------------|--------------|------------------|------------------|----------------|
| EPIC002: Service deployment | FEA005: Automate build,test, and deployment process                                                    | X       | A        | 2                | 2      | 10               | 6       | 2              | 2          | 24           | 2 190,00 €       | 2 518,50 €       | 3 160,72 €     |
|                             | FEA004: Implement CI/CD pipelines for all services                                                     |         | B        | 2                | 3      | 9                | 5       | 2              | 1          | 22           | 2 030,00 €       | 2 334,50 €       | 2 930,48 €     |
| EPIC003: Prestashop as service| FEA006: Provide managed hosting for Prestashop instances                                              | X       | A        | 4                | 4      | 10               | 6       | 2              | 3          | 29           | 2 370,00 €       | 2 725,50 €       | 3 419,03 €     |
|                             | FEA007: Dockerized Service Production                                                                  |         | A        | 4                | 4      | 8                | 6       | 2              | 2          | 26           | 2 175,00 €       | 2 501,25 €       | 3 138,06 €     |
|                             | FEA008: Secure Service Access                                                                          |         | B        | 4                | 2      | 4                | 3       | 2              | 2          | 17           | 1 840,00 €       | 2 116,00 €       | 2 655,58 €     |
|                             | FEA078: Server management & Backup                                                                     |         | B        | 3                | 2      | 4                | 3       | 2              | 2          | 16           | 1 710,00 €       | 1 966,50 €       | 2 467,96 €     |
|                             | FEA009: Provide API access for developers to integrate with other services                             |         | B        | 3                | 3      | 10               | 4       | 2              | 2          | 24           | 2 250,00 €       | 2 587,50 €       | 3 254,31 €     |
| EPIC004: Log management     | FEA010: Provide real-time log monitoring and analysis capabilities                                     | X       | A        | 10               | 3      | 14               | 10      | 2              | 4          | 43           | 3 630,00 €       | 4 174,50 €       | 5 243,93 €     |
| EPIC005: Security Enhancements | FEA011: Implement security controls (e.g., run as non-root, enhance container security)                | X       | A        | 8                | 2      | 12               | 8       | 2              | 2          | 34           | 2 970,00 €       | 3 415,50 €       | 4 291,73 €     |
|                                | FEA015: Implement PrestaScan Security on SaaS Prestashop                                                | X       | B        | 10               | 2      | 12               | 12      | 2              | 2          | 40           | 3 330,00 €       | 3 829,50 €       | 4 808,21 €     |
|                                | FEA016: Set up the security module                                                                      | X       | C        | 6                | 3      | 12               | 8       | 2              | 3          | 34           | 2 880,00 €       | 3 312,00 €       | 4 159,56 €     |
|                                | FEA020: Database security hardening                                                                     | X       | C        | 16               | 3      | 12               | 6       | 2              | 2          | 41           | 3 250,00 €       | 3 737,50 €       | 4 681,31 €     |
| EPIC006: Test Automation       | FEA022: Acceptance Test Automation                                                                      | X       | A        | 8                | 2      | 14               | 12      | 2              | 2          | 40           | 3 290,00 €       | 3 783,50 €       | 4 741,59 €     |
|                                | FEA023: Integrate test automation into the CI/CD pipeline                                               | X       | B        | 6                | 2      | 12               | 10      | 2              | 2          | 34           | 2 870,00 €       | 3 300,50 €       | 4 140,88 €     |
| EPIC007: Bug fixes             | FEA028: Ensure efficient bug reporting and triage processes                                             | X       | A        | 2                | 2      | 6                | 6       | 2              | 1          | 19           | 1 680,00 €       | 1 932,00 €       | 2 423,66 €     |
|                                | FEA029: Utilize error tracking tools to proactively identify and address issues                        | X       | A        | 2                | 2      | 6                | 6       | 2              | 1          | 19           | 1 680,00 €       | 1 932,00 €       | 2 423,66 €     |
|                                | FEA030: Integrate with version control systems (e.g., Git)                                              | X       | A        | 2                | 2      | 8                | 4       | 2              | 2          | 20           | 1 820,00 €       | 2 093,00 €       | 2 624,72 €     |
|                                | FEA031: Assign bugs to developers and track progress towards resolution                                | X       | A        | 4                | 2      | 6                | 4       | 2              | 2          | 20           | 1 800,00 €       | 2 070,00 €       | 2 596,85 €     |
| EPIC008: Registration and login| FEA035: Secure user login                                                                               | X       | A        | 4                | 2      | 6                | 4       | 2              | 2          | 20           | 1 800,00 €       | 2 070,00 €       | 2 596,85 €     |
|                                | FEA036: Password recovery                                                                               | X       | A        | 4                | 2      | 6                | 4       | 2              | 2          | 20           | 1 800,00 €       | 2 070,00 €       | 2 596,85 €     |
| EPIC009: Service Backup        | FEA039: Automated Database Backup. Implement automated scheduling for regular database backups         | X       | A        | 4                | 2      | 8                | 6       | 2              | 2          | 24           | 2 130,00 €       | 2 449,50 €       | 3 072,79 €     |
|                                | FEA040: Implement automated backups of the entire Prestashop installation, including files, images, and themes | X   | B        | 4                | 2      | 8                | 6       | 2              | 2          | 24           | 2 130,00 €       | 2 449,50 €       | 3 072,79 €     |
| EPIC010: Performance Tuning    | FEA045: Page Caching: implement efficient page caching mechanisms                                       | X       | A        | 4                | 2      | 8                | 4       | 2              | 2          | 22           | 1 960,00 €       | 2 254,00 €       | 2 825,93 €     |
| EPIC011: Customer Feedback     | FEA058: Customer Feedback Forms                                                                         | X       | A        | 2                | 2      | 6                | 2       | 2              | 2          | 16           | 1 570,00 €       | 1 805,50 €       | 2 265,97 €     |
| EPIC015: Documentation & Training | FEA062: General Documentation                                                                       | X       | A        | 2                | 2      | 6                | 2       | 6              | 2          | 22           | 1 910,00 €       | 2 196,50 €       | 2 757,79 €     |
|                                | FEA071: Implement and maintain data privacy policies and procedures in line with relevant regulations  | X       | A        | 2                | 2      | 6                | 2       | 6              | 2          | 22           | 1 910,00 €       | 2 196,50 €       | 2 757,79 €     |
|                                | FEA073: Clear crisis communication guidelines and practices                                            | X       | A        | 2                | 2      | 6                | 2       | 6              | 2          | 22           | 1 910,00 €       | 2 196,50 €       | 2 757,79 €     |
|                                | FEA074A: A Risk Management Checklist for Prestashop                                                    | X       | A        | 2                | 2      | 6                | 2       | 6              | 2          | 22           | 1 910,00 €       | 2 196,50 €       | 2 757,79 €     |
| **TOTAL**                     |                                                                                                          |         |          |                  |        |                  |         |                |            | **598**      | **59 338,00 €**  | **68 238,70 €**  | **85 293,88 €**|

<!--
|Description |	In Plan |	Priority |	Total Hours |	Total Work Price |	+15% Profit |	+VAT 25% |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|FEA010: Integrate with a vulnerability scanning tool to automatically detect and report known vulnerabilities|	YES|	P2|40|2 525,00 €|	|2 903,75 €|	|3 629,69 €|
|FEA021: Implement CI/CD pipelines for all services.	|YES	|P3|26|1 595,00 €|	1 834,25 €|	2 292,81 €|
|FEA022: Automate build, test and deployment processes|	YES|	P3|25|1 575,00 €|	1 811,25 €|	2 264,06 €|
|FEA002: Secure Service Access	|YES	|P1|14|895,00 €|	1 029,25 €|	1 286,56 €|
|FEA003: Dockerized Service Production	|YES	|P1|28|1 705,00 €|	1 960,75 €|	2 450,94 €|
|FEA031: Provide managed hosting for Prestashop Instances|	YES|	P1|24|1 510,00 €|	1 736,50 €|	2 170,63 €|
|FEA032: Provide API access for developers to integrate with other services|	YES|	P1|31|1 915,00 €|	2 202,25 €|	2 752,81 €|
|FEA063: Integrate test automation into the CI/CD pipeline|	YES|	P4|24|1 455,00 €|	1 673,25 €|	2 091,56 €|
|FEA067: Acceptance test Automation|	YES|	P4|27|1 690,00 €|	1 943,50 €|	2 429,38 €|
|FEA086: Perform regression testing after bug fixes to ensure that the fix did not introduce new issues|	YES|	P4|27|1 690,00 €|	1 943,50 €|	2 429,38 €|
|FEA217: Automated Testing: Faciliate automated testing within the Docker environment (e.g. Test automation tools)|	YES|	P4|25|1 585,00 €|	1 822,75 €|	2 278,44 €|
|FEA004: Customer segmentation	|YES	|P5|45|2 855,00 €|	3 283,25 €|	4 104,06 €|
|FEA181: Detailed sales reports	|YES	|P5|45|2 855,00 €|	3 283,25 €|	4 104,06 €|
|FEA182: Shopping cart abandonment analysis|	YES|	P5|45|2 855,00 €|	3 283,25 €|	4 104,06 €|
|FEA183: Real-Time Analytics|	YES	|P5|44|2 795,00 €|	3 214,25 €|	4 017,81 €|
-->

**Division of labor:**

|Task|Total hours in category|
|:-:|:-:|
|Project management	|145|
|Server maintanance/administration|125|
|Familiarization|400|
|Planning	|226|
|Implementation	|308|
|Documentation	|336|
|Testing	|222|
|Meetings	|408|
|Other|	65|

[Cost estimation Sheets](assets/cost_estimate.ods)

### Work cost estimation

|||
|:-:|:-:|
|Total Project Working Hours|2235 h|
|TOTAL WORK COST|136 210,00 €|
|Total work cost with Profit 15 %|156 641,50 €|
|Total work cost with Profit incl. 25,5% VAT|196 585,08 €|

### Feature costs

|||
|:-:|:-:|
|Estimated feature hours|598 h|
|TOTAL FEATURE COST|59 338,00 €|
|Total work cost with Profit 15 %|68 238,70 €|
|Total work cost with Profit incl. 25,5% VAT|85 298,38 €|

## 5. Supplier Introduction

* Your Team: [DevLetics team introduction](https://core-e28f4a.pages.labranet.jamk.fi/10-Project-management/team-introduction/)
* For more info, contact: AH0986@student.jamk.fi

## 6. Other things to consider

* limited to JAMK's ICT student courses
* user numbers limited to JAMK's ICT students
* contacts are requested primarily by Discord, secondarily by email
* the offer is valid until 30.6.2025
