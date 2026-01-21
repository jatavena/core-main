# Master Test Plan

|  |  |
|:-:|:-:|
| Document | Master Test Plan |
| Author: | Juha Sirnio - Tester, Teemu Vitikainen - Tester |
| Version: | v0.3 |
| Date: | 13.08.2025 |

<!-- >## General information --> 

<!-- >A master test plan (MTP) is a high-level document that describes the overall testing strategy, objectives, and scope for a software project or product. It provides a comprehensive overview of the key decisions, resources, risks, and deliverables involved in the testing process. It also defines the relationship and coordination among different test levels, such as unit testing, integration testing, system testing, and acceptance testing. An MTP helps to ensure that the testing activities are aligned with the project goals and requirements, and that the quality of the software is verified and validated. You can find more information about MTPs from these sources:

- [What are Master Test Plans & Level Test Plan? Examples, When to use. ](http://tryqa.com/what-are-master-test-plans-level-test-plan-examples-when-to-use/)
- [Developing a Test Plan: A Complete Guide](https://tech-stack.com/blog/test-plan/)
- [What is a Test Plan in Software Testing? - TestLodge blog](https://blog.testlodge.com/what-is-a-test-plan-in-software-testing/)
- [Why Every QA Team Needs To Create Master Test Plan?](https://www.qatouch.com/blog/why-every-qa-team-needs-to-create-master-test-plan/)
- [https://www.scaler.com/topics/software-testing/test-plan-in-software-testing/(https://www.scaler.com/topics/software-testing/test-plan-in-software-testing) 
- [https://www.lambdatest.com/learning-hub/test-plan](https://www.lambdatest.com/learning-hub/test-plan) -->



<!-- ># Master Test Plan -->

## 1. Introduction
<!-- >Briefly describe the purpose of the document, the system under test, and the scope of the testing activities. -->

This document presents the testing strategy, objectives, and coverage plan for the PrestaShop e-commerce platform. Its primary goal is to validate that all implemented features meet both functional and non-functional requirements, while upholding the overall quality of the system.

Testing is conducted to confirm that the platform is both stable and dependable prior to its release, minimizing the risk of issues in the production environment.

The system under test is a containerized PrestaShop instance deployed on CSC Pouta, integrated with MySQL, and managed via Docker. The platform supports secure functionalities, automated GitLab CI/CD pipelines, real-time logging, and robust user and developer-facing features.

## 2. Test Objectives
<!-- >Define the goals and objectives of the testing activities.-->

The testing process focuses on three core objectives: ensuring that newly added features perform correctly across different scenarios, confirming that existing functionalities remain unaffected by recent changes, and identifying potential issues early in development to uphold system reliability and overall quality.

<!-- >- Test user workflows (login, order, register) -->
<!-- >- Verify automation of CI/CD pipeline and Docker builds -->
<!-- >- Validate secure access (HTTPS, non-root containers) -->
<!-- >- Confirm real-time logging and alerting -->
<!-- >- Added security features and modules -->

## 3. Test Items
<!-- >List the software items that will be tested. -->

Test items based on the features being implemented:

- **Service deployment** - Establish CI/CD pipelines to streamline and automate the build, test, and deployment processes across all services

- **PrestaShop as service** - Deliver secure, containerized hosting and service access for PrestaShop, with automated server management and production-ready infrastructure

- **Log management** - Using real-time logs, monitoring and analysis

- **Security enhancements** - Enhance PrestaShop security by integrating PrestaScan, configuring security modules, and applying container hardening practices

- **Test automation** - Automate acceptance testing and integrate it seamlessly into the CI/CD pipeline to ensure continuous validation of application functionality

- **Registration and login** - Implement secure user authentication and recovery mechanisms to protect account access and ensure user convenience 

- **Service backup** - Automate regular backups of the PrestaShop database and installation, including files and media, with scheduled processes to ensure data integrity and recovery readiness

- **Security fixes** - Implement measures to safeguard servers and services against malicious traffic and unauthorized access.


<!-- >- **Functionality & Security** - Secure login/password recovery and Service usage -->

<!-- >- **Security features** - Such as installed tools, modules, vulnerability scanning and security hardening -->

<!-- >- **Using real-time logs** - monitoring and analysis -->

<!-- >- **PrestaShop as service and customer engagement** – User workflows and customer support system functions  -->

<!-- >- **Operational efficiency** – Automation of CI/CD pipeline (build, testing and deployment) -->

<!-- >- **Dockerized service production** - PrestaShop + MySQL -->

<!-- >- **Recovery readiness** - Automated backups -->

<!-- >- **Internal operations** - Server management -->

<!-- >- Verifying Dockerized PrestaShop + MySQL container setup -->
<!-- > - Verifying Secure Access (HTTPS, non-root containers) -->
<!-- > - Verifying Automation of CI/CD pipeline and Docker builds -->
<!-- > - Testing Added Security features and modules -->
<!-- > - Ensuring user workflows (login, order, register) -->
<!-- > - Testing the Customer Engagement functions --> 
<!-- > - Ensuring real-time logging and alerting -->
<!-- > - Verifying Automated backups entire PrestaShop installation -->

<!-- >- Dockerized PrestaShop + MySQL container setup -->
<!-- >- GitLab CI/CD pipeline for automated deployment -->
<!-- >- User workflows (PrestaShop UI) -->
<!-- >- HTTPS/SSL setup -->
<!-- >- Log monitoring system -->
<!-- >- Installed security modules -->
<!-- >- Host-Level Security -->

## 4. Features to be Tested
<!-- >Describe the features of the software that will be tested. -->

Service deployment

- FEA004 Implement CI/CD pipelines for all services
- FEA005 Automate build, test, and deployment processes

PrestaShop as service

- FEA006 Provide managed hosting for PrestaShop instances
- FEA007 Dockerized Service Production
- FEA008 Secure Service Access
- FEA078 Server management

Log management

- FEA010 Provide real-time log monitoring and analysis capabilities

Security enhancements

- FEA015 Implement PrestaScan Security to scan PrestaShop website
- FEA016 Set up the security modules
- FEA017 Implement security contexts (e.g., run as non-root user) to enhance container security

Test automation

- FEA022 Acceptance Test Automation
- FEA023 Integrate test automation into the CI/CD pipeline

Registration and login

- FEA035 Secure user login
- FEA036 Password recovery

Service backup

- FEA039 Automated Database Backup. Implement automated scheduling for regular database backups
- FEA040 Implement automated backups of the entire PrestaShop installation, including files, images, and themes

Security fixes

- FEA097 protect server and services from malicious traffic 


<!-- >Functionality & Security-->

<!-- >- FEA035 Secure user login -->
<!-- >- FEA036 Password recovery -->
<!-- >- FEA008 Secure Service Access -->

<!-- >Security features -->

<!-- >- FEA017 Implement security contexts (e.g., run as non-root user) to enhance container security -->
<!-- >- FEA015 Implement PrestaScan Security to scan PrestaShop website -->
<!-- >- FEA016 Set up the security modules -->
<!-- >- FEA097 protect server and services from malicious traffic  -->

<!-- >Using real-time logs -->

<!-- >- FEA010 Provide real-time log monitoring and analysis capabilities -->

<!-- >PrestaShop as service and customer engagement -->

<!-- >- FEA006 Provide managed hosting for PrestaShop instances -->

<!-- >Operational efficiency -->

<!-- >- FEA004 Implement CI/CD pipelines for all services -->
<!-- >- FEA005 Automate build, test, and deployment processes -->
<!-- >- FEA023 Integrate test automation into the CI/CD pipeline -->
<!-- >- FEA022 Acceptance Test Automation  -->

<!-- >Dockerized service production -->

<!-- >- FEA007 Dockerized Service Production -->

<!-- >Recovery readiness -->

<!-- >- FEA039 Automated Database Backup. Implement automated scheduling for regular database backups -->
<!-- >- FEA040 Implement automated backups of the entire PrestaShop installation, including files, images, and themes -->

<!-- >Internal operations -->

<!-- >- FEA078 Server management -->


<!-- >- FEA023 User workflows -->
<!-- > - FEA008 Secure Service Access  -->
<!-- > - FEA005 Automate build, test, and deployment processes -->
<!-- > - FEA017 Implement security contexts (e.g., run as non-root user) to enhance container security -->
<!-- > - FEA007 Dockerized Service Production -->
<!-- > - FEA010 Provide real-time log monitoring and analysis capabilities -->
<!-- > - FEA006 Provide managed hosting for PrestaShop instances -->


## 5. Features not to be Tested
<!-- >Describe any features of the software that will not be tested and explain why. -->

These features were not targeted by test cases:

- FEA028: Ensure efficient bug reporting and triage processes
- FEA030 Integrate with version control systems (e.g., Git)
- FEA031 Assign bugs to developers and track progress towards resolution
- FEA062 General documentation


<!-- >Deep testing of internal PrestaShop modules -->

## 6. Approach
<!-- >Outline the overall approach to testing. Include the types of testing that will be performed (e.g., unit, integration, system, acceptance) and any testing tools that will be used. -->

Testing activities will incorporate a blend of manual and automated methods, allowing for comprehensive evaluation of the system from both functional and efficiency perspectives.

Key types:

- Manual Testing: This involves checking the functionality of newly developed features and performing exploratory testing to uncover unexpected issues.
- Regression Testing: Automated tests, implemented with the Robot Framework, will be used to verify that existing features continue to operate correctly after updates.

Additionally, non-functional Testing: Performance assessments will be conducted to measure the system’s responsiveness, reliability, and ability to scale effectively.

| Testing types |                         |
|----------|--------------------------------------|
| Integration Testing  | Validate service interactions                 | 
| System Testing  |  Real flows | 
| Security Testing   | e.g. Container vulnerabilities             | 
| Regression Testing   | Re-run tests after bug fixes or updates                | 
| Manual Testing   | Functional validation and Exploratory Testing                | 

<!-- >Full platform tests with real-world flows -->
<!-- >Validate service interactions PrestaShop - MySQL -->
<!-- > and login mechanisms -->
<!-- >ssl -->

| Tools |                         |
|----------|--------------------------------------|
| Robot Framework  | Regression testing & UI automation                 | 
| GitLab CI/CD | Automated pipeline validation | 
| Performance testing   |  K6           | 
        

## 7. Item Pass/Fail Criteria
<!-- >Define the criteria that will be used to determine whether each software item has passed or failed its tests. -->

| Test Item  | Pass Criteria                          |
|----------|--------------------------------------|
| Functional Test  | Meets acceptance criteria and expected behavior                 | 
| CI/CD Pipeline   | Successful build/test/deploy without errors| 
| Security   | No critical vulnerabilities in containers                | 

<!-- >Log Monitoring   Real-time logging + alerting work as expected -->

## 8. Suspension Criteria and Resumption Requirements
Testing will be suspended if critical infrastructure (Docker, MySQL, CSC Pouta) is unavailable or blocking defects prevent further testing.
Testing resumes when blocking issues are resolved and the environment is restored.

## 9. Test Deliverables
- Master Test Plan (this document)
- Test cases
- Failed/Unconfirmed test cases
- Defect/bug reports
- Summary report at project end
- Installation and user documentation (if required)

<!-- Test execution reports -->

## 10. Testing Tasks

- Prepare and review the test plan
- Design and document test cases
- Execute test cases
- Report and track defects
- Retest after bug fixes
- Prepare test summary and closure reports
- Communicate with members and project supervisor

<!-- Set up the test environment (CSC Pouta, Docker, PrestaShop, MySQL) -->

## 11. Environmental Needs
- CSC Pouta virtual machine with Ubuntu Linux
- Docker and Docker Compose installed
- MySQL database (development and staging environment)
- PrestaShop (development and staging versions)
- GitLab for version control and issue tracking
- Browsers for UI testing (Chrome, Firefox, etc.)
- Test data (users, products, orders)
- Robot Framework installed & k6 

## 12. Responsibilities
- Tester: Juha Sirniö – executes tests, reports defects | Testing tasks
- Tester: Teemu Vitikainen – executes tests, reports defects | Testing tasks
- Team Lead: reviews progress, verify
- Developers: fix defects, support test environment setup, verify
- DevOps/Environment: (if separate) – maintains test environment, verify
- Security engineer/officer: sec features implementation, verify, auditing

<!-- Project Supervisor: reviews progress, approves deliverables -->

## 13. Staffing and Training Needs
- Two testers (both beginners)
- Training on PrestaShop basics, Robot Framework, Docker usage, and GitLab workflows
- Guidance from supervisor or experienced team members as needed

## 14. Schedule
- Sprint 02 start: 16.06.2025 - 28.06.2025
- Test planning: 16.06.2025 - 
- Test case design: 01.07.2025 -
- Test execution: 01.07.2025 -
- Bug fixing and retesting: 01.07.2025 -
- Project end: 29.08.2024

<!-- Acceptance testing: [date range] -->

## 15. Risks and Contingencies
- Limited testing experience (mitigation: training, supervisor support)
- Environment setup delays (mitigation: early setup, backup plans)
- Unforeseen technical issues with Docker, PrestaShop, or CSC Pouta (mitigation: document issues, seek help early)
- Incomplete requirements or scope changes (mitigation: clarify with supervisor, document changes)

## 16. Approvals
- Testers: Teemu Vitikainen, Juha Sirniö
- Team Lead and members

<!--Project Supervisor: Okko Tuuri -->
<!-- Developers: Tugba Ilhan -->