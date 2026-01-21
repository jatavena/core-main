# Test Report

|  |  |
|:-:|:-:|
| Document | Test Report |
| Author: | Juha Sirnio - Tester, Teemu Vitikainen - Tester  |
| Version: | v0.1 |
| Date: | 18.8.2025 |

<!-- >## 1. Introduction
Briefly describe the purpose of the document and the system under test.

## 2. Test Items

List the software items that were tested.

## 3. Test Levels 

Describe the different levels of testing that were performed (e.g., unit, integration, system, acceptance).

## 4. Test Cases
For each test case, provide the following information:
- Test Case ID
- Test Case Description
- Test Level
- Test Environment
- Test Execution Date and Time
- Expected Results
- Actual Results
- Pass/Fail --> 

## 1. Test Summary
<!-- >Provide a summary of the testing activities, including the number of test cases passed, failed, and skipped. -->

Summary of testing activity, including passed and planned. Tracking of failed/unconfirmed test cases and bugs.

<!-- >Summary of testing activities, including passed, planned, failed/unconfirmed test cases and bug tracking. -->

**PASSED** - test cases 

| ID  | Feature  | Test case  | Version  | Expected result  |
|--|--|--|--|--|
| 233  | FEA035 | Verify HTTPS is Enabled Across All Login-Related Pages  | 0.1 | - Login page uses HTTPS. - Any HTTP request is redirected to HTTPS. - No mixed content warnings are displayed in the browser. |
| 234  | FEA035 | Verify User Can Log In with Valid Credentials and Establish Secure Session  | 0.1 | - User logs in successfully. - Session is established securely (cookie flags present). - User is redirected to the homepage, and “Sign Out” is displayed in the header. |
| 235  | FEA035 | Verify Login Form Rejects Invalid Credentials with Appropriate Error Messages | 0.1 | - Login fails. - An error message such as “Authentication failed” is displayed. - The error message does not reveal which field was incorrect (to prevent enumeration attacks). |
| 236  | FEA035 | Verify Sensitive User Data Is Not Transmitted or Stored in Plain Text  | 0.1 | - No sensitive data (passwords, session tokens) are transmitted or stored in plaintext. - All communication is encrypted. |
| 256  | FEA035 | Verify secure Admin login with valid credentials  | 0.1 | - Admin user logs in successfully. - Session is established securely (cookie flags present). - User is redirected to the dashboard. |
| 257  | FEA035 | Verify Admin Login Form Rejects Invalid Credentials with Appropriate Error Messages  | 0.1 | - Login fails. - An error message such as “Authentication failed” is displayed. - The error message does not reveal which field was incorrect (to prevent enumeration attacks). |
| 242  | FEA015 | Verify PrestaScan Security is Successfully Integrated and Scans Periodically | 0.1 | - Scan history shows timestamps indicating scans are functioning. - Can trigger a manual scan. |
| 243  | FEA015 | Verify Known Vulnerabilities are Detected and Listed in Report | 0.1 | - A report is generated listing: Known vulnerabilities detected. - Each item includes severity (Low, Medium, High) and location. |
| 245  | FEA015 | Verify Guidance or Recommendations are Provided for Detected Issues | 0.1 | - Each detected issue includes:A description of the issue. Impact and severity. Recommendations or documentation links for remediation. |
| 251  | FEA016 | Verify Security Modules Can Be Installed and Activated | 0.1 | - Both Simple Security and eiCAPTCHA are installed and active. - No conflicts or errors occur on the frontend while browsing. |
| 252  | FEA016 | Verify Security Modules Can Be Configured and Protect  | 0.1 | - Simple Security configuration is saved and active. - eiCAPTCHA is active, and reCAPTCHA is displayed on login/register forms. |
| 253  | FEA016 | Verify Brute-Force Blocking by Simple Security | 0.1 | - The system blocks login attempts (8) and displays a lockout message. - Admin backoffice logs record the brute-force attempt |
| 254  | FEA016 | Verify reCAPTCHA Enforcement by eiCAPTCHA | 0.3 | - reCAPTCHA is displayed consistently on register forms. - Form submissions fail when reCAPTCHA is not solved. - Form submissions succeed when reCAPTCHA is correctly solved. - No conflicts with other modules (e.g., forms still submit properly with reCAPTCHA enabled) |
| 255  | FEA016 | Verify Logging/Blocking of SQL Injection Attempts by Simple Security  | 0.1 | - SQL injection attempts are blocked, logged or input sanitized. - The system remains stable, with no crashes or frontend/backend errors. |
| 272  | FEA022 | Verify Robot Framework Setup and Execution  | 0.1 | - Robot Framework executes the test file without errors. - Test results are generated (e.g., log.html, report.html). |
| 273  | FEA022 | Verify Custom Test Case Creation, Execution, and Reporting  | 0.1 | - The custom test case runs successfully. - Results are reported in the test output (log.html, report.html). - Testers can review the results and logs for each test execution. |
| 274  | FEA022 | Verify Automated Product Page Load  | 0.1 | - All product pages load successfully without errors. - Any failed page loads are reported in the test output. |
| 275  | FEA022 | Verify Error Messages and Screenshots on Failure | 0.1 | - Clear error messages and screenshots are available for failed tests in the log.html. |
| 276  | FEA022 | Verify CI/CD Integration | 0.1 | The Product pages test. - The test files run automatically on each build or deployment. - Results are visible in the CI/CD pipeline logs or reports. |
| 246  | FEA036 | The reset process works correctly across different devices (mobile, tablet, desktop) | 0.1 | - The user can successfully reset their password on all devices. - The user interface and functionality are consistent across devices. |
| 240  | FEA036 | Request password reset via registered email | 0.1 | - The system confirms that a password reset email has been sent to the provided address. - No information is leaked about whether the email is registered or not (for security). |
| 247  | FEA036 | Invalid or expired reset links show appropriate error messages | 0.1 | - The system displays a clear error message in each case. - No information is revealed to the user about whether the link was ever valid. |
| 289  | FEA006 | Verify Submit Support Request via Contact Us Page  | 0.1 | - A confirmation message appears: "Your message has been successfully sent to our team." - The sender of the message receives a response from customer service in their email. |
| 277  | FEA023 | Verify Automated Tests Trigger on Each CI/CD Pipeline Run  | 0.1 | - Tests execute automatically in the pipeline. - Tests run without manual intervention after push. - Tests are executed consistently across branches and merge requests. |
| 278  | FEA023 | Verify Generation of Detailed Test Reports After Pipeline Run  | 0.1 | - A detailed, structured test report is generated (report.html, log.html). - It shows passed and failed test cases clearly. - Test report is stored as an artifact in the GitLab CI/CD pipeline and can be downloaded/viewed in the GitLab interface. - Failure stack traces and screenshots (if included) are present for debugging. |
| Planned  |  |   |  |  |
| 238  | FEA005 | Automated Tests Triggered After Successful Build   |  | - After the build completes, automated tests are triggered automatically. - Test results are reported in the pipeline. - No manual triggering of tests is required. |
| 259  | FEA004 | Verify Automatic Regression and Other Tests    |  | - Regression and other defined tests are triggered automatically after the build. - Test results are reported in the pipeline system. - If any test fails, the deployment stage does not start (unless intended) |
| 260  | FEA004 | Verify notifications on Build or Test Failures    |  | - The team leader immediately receives a notification about the failed build or test. - The notification includes details about the failed stage and, if possible, a link to the pipeline logs. |
| 270  | FEA078 | Verify Webmin Secure Access via HTTPS with Proper Certificates     |  | - Webmin is accessible only via HTTPS. - Certificates are correctly applied and valid. - Unencrypted HTTP access is blocked or redirected. |

| ID  | Feature  | Test case  | Version  | Expected result  |
|--|--|--|--|--|
| 249  | FEA017 | Verify Trivy Scans Run During CI/CD Pipeline Build   | 0.1 | - Trivy scan runs automatically in the pipeline. - Detected vulnerabilities are listed in the pipeline logs with severity details. (Secure > Vulnerability Report) - Pipeline status reflects passed/failed depending on vulnerability threshold. |
| 261  | FEA007 | Verify Availability and Completeness of PrestaShop Docker Image   | 0.1 | - The Docker image builds/pulls successfully and starts without errors. - All required PHP extensions are present, ensuring compatibility with PrestaShop development. |
| 262  | FEA007 | Verify Live Local Code Mounting via Docker Volume   | 0.1 | - The change is reflected immediately without needing to restart the container. - No permission or sync issues occur. |
| 263  | FEA007 | Verify MySQL Integration with Docker Compose    | 0.1 | - PrestaShop connects to MySQL and completes installation successfully. - Admin and storefront load properly with data persisted in MySQL. |
| 279  | FEA010 | Verify Real-Time Log Access and Filtering for Developers    | 0.1 | - Developer can access real-time logs from running containers/services. - Logs include timestamps, severity, and component info. - Logs can be filtered by service/module or keyword. - Logs are accessible via CLI (Docker) and/or PrestaShop dashboard. - Unauthorized access to logs is prevented. - Developer can trace an error through the logs. |
| 280  | FEA010 | Verify Log Insights and Visualization in PrestaShop Dashboard  | 0.1 | - Product Owner can access log data and summaries via the PrestaShop dashboard. - Logs are updated in near real-time and can be filtered. - Dashboard provides at least basic insights (counts, error levels, recent issues). - Information is sufficient to support data-driven decisions about platform improvements.   |
| 282  | FEA097 | Verify Fail2Ban service installation and active status | 0.1 | - Fail2Ban service is active (running). - Service is enabled to start on boot.   |
| 283  | FEA097 | Verify Fail2Ban service installation and active status | 0.1 | - Fail2Ban detects repeated failed SSH login attempts. - The offending IP is banned and cannot SSH into the server during the ban period. - After the ban period, the IP is automatically unbanned.   |
| 285  | FEA097 | Verify Fail2Ban logging for review   | 0.1 | - Logs clearly show: Which IPs were banned. - Which jail triggered the ban. - Timestamps of bans and unbans. - Logs are accessible for ongoing monitoring and audit.   |
| 290  | FEA006 | K6-Frontpage-LoadTest   | 0.1 | - Availability: At least 99% of requests return HTTP 200 OK during the test duration. - Performance: 95% of response times are less than 2 ms. No more than 1% of requests fail. - Stability: No unexpected server errors (HTTP 5xx) or connection resets occur during the test. - Completion: Test completes without premature termination or critical errors in K6 execution.   |
| 291  | FEA039 | Verify that a store owner can securely and reliably store backups in a chosen location    | 0.1 | - The backup is saved in the selected location.  |
| 293  | FEA039 | Verify that a store owner can schedule automated backups of their PrestaShop database and files    | 0.1 | - A new backup appears automatically at the scheduled time.  |
| 292  | FEA040 | Automatic Full Backups Are Created at Scheduled Intervals   | 0.1 | - A timestamped backup contains all expected data.  |
| 294  | FEA040 | Integration of Custom Backup & Recovery Scripts    | 0.1 | - Scripts run without errors and backup/restore succeed.  |
| Planned  |  |   |  |  |
| 237  | FEA005 | Rollback Deployment Without Service Interruption   |  | - The rollback process starts quickly (e.g., within 2 minutes). - The service remains available throughout the rollback. - The previous version is restored successfully and the error situation is resolved. |
| 239  | FEA005 | Team Leader Receives Notifications on Build or Test Failures    |  | - The team leader receives a notification about the build failure. - The team leader receives a notification about the test failure. - Notifications contain sufficient information to identify the problem (e.g., build/test logs, commit ID). |
| 258  | FEA004 | Verify that a developer can deploy code changes to production with a single click   |  | - The deployment process starts automatically with a single click. - No manual intermediate steps are required. - The production environment is updated with the new code. - The process completes successfully and quickly. |
| 271  | FEA004 | Verify deployment to multiple environments   |  | - The code is deployed to both staging and production environments without errors. - Each deployment step is logged and traceable in the pipeline system. - The application is accessible and functional in both environments after deployment. - Any errors or failures are clearly reported in the pipeline logs and notifications. |
| 264  | FEA007 | Verify Containerized Development Workflow    |  | - Development workflow functions smoothly within containers. - Changes reflect instantly, and PrestaShop operates as expected within the container environment. |
| 265  | FEA007 | Verify Service Operation in Containers     |  | - Services run reliably in containers with consistent behavior during stop/start cycles. - Data is persisted across container lifecycles. - PrestaShop operates without issues in a containerized environment. |
| 266  | FEA078 | Verify Webmin Installation and Browser Accessibility      |  | - Webmin installation completes without errors. - Webmin is accessible via a browser on https:// :10000. - The Webmin login page loads without SSL errors (or with expected cert warnings if using self-signed temporarily). |
| 267  | FEA078 | Verify Webmin Authentication and Access Control       |  | - Login is successful only with valid administrator credentials. - Login fails with invalid credentials or unauthorized users. - Brute-force lockout, if configured, activates after repeated failed attempts. |
| 268  | FEA078 | Verify Core Webmin Functionality (Service, Monitoring, User Management)      |  | - Administrator can start/stop services through Webmin. - Resource usage statistics display accurately. - Administrator can create and delete system users. |
| 269  | FEA078 | Verify Webmin Logging and Auditability      |  | - All user actions in Webmin are logged in the Webmin Actions Log. - Access attempts are recorded in system logs. - Logs include timestamps, user identifiers, and actions performed. |

**Tracking** - Failed/unconfirmed test cases and bugs

|  |   |  |   |   |
|--|--|--|--|--|
| 254  |  |   |  |  |





<!-- >## 6. Defects

For each defect found, provide the following information:


| Defect ID | Defect Short Description |
|:-:|:-:|
| #13 | Example of the Bug/Defect issue | 
| #13 | Example of the Bug/Defect issue | 
| #13 | Example of the Bug/Defect issue | 
| #13 | Example of the Bug/Defect issue | 
| #13 | Example of the Bug/Defect issue | 
| #13 | Example of the Bug/Defect issue | 




## 7. Conclusion
Summarize the overall quality of the system based on the test results.

## 8. Recommendations
Provide any recommendations for future testing activities or improvements to the system.

## 9. Approvals
Specify who must approve the report. --> 
