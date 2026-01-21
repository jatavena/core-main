# Security Features Documentation

| | |
|:------: |:--: |
| Document | Security features document for ECSP1 Project |
| Author:  | Jarmo Venäläinen (security) |
| Version: | v 0.6.5 |
|  Date:   |  25.7.2025 |

## Contents

1. [Introduction](#1-introduction)
2. [CI/CD Pipeline Security](#2-cicd-pipeline-security)
3. [Architecture-Level Security](#3-architecture-level-security)
4. [Server-Level Hardening](#4-server-level-hardening)
5. [Application-Level Protection](#5-application-level-protection)
6. [User Data & Privacy (GDPR)](#6-user-data--privacy-gdpr)
7. [Authentication & Access Control](#7-authentication--access-control)
8. [Additional Recommendations](#8-additional-recommendations)
9. [Contact](#9-contact)

## 1. Introduction

This document outlines the main technical security features and policies regarding their use implemented in the service and its production. It also includes setup and configuration instructions for some of the features and descriptions of their current configurations.  

It is intended to provide transparency and clarity for developers, administrators, auditors, and other stakeholders. Clear and up-to-date documentation helps ensure that security is embedded into the service from the beginning and maintained throughout its lifecycle.

---
## 2. CI/CD Pipeline Security

### 2.1 GitLab CI/CD
#### 2.1.1 GitLab automation

Our project uses a CI/CD pipeline (Continuous Integration / Continuous Deployment) to automate the building, testing, and deployment of the software. CI/CD ensures that code changes are regularly integrated and safely delivered to production, improving development speed and reliability. From a security perspective, early detection of vulnerabilities during this pipeline is critical. Issues found earlier are cheaper and easier to fix than those discovered later in production. Integrating these scans directly into the CI/CD pipeline enables a proactive security approach that prevents vulnerabilities from ever reaching production.

Our CI/CD pipeline leverages some of GitLab’s built-in automated security tools, configured through `.gitlab-ci.yml` files. The following GitLab features are in use:
- **SAST (Static Application Security Testing)** scans the source code for vulnerabilities before the application is even run. It detects issues like unsafe input handling or insecure function usage.
- **Secret Detection** searches the codebase for accidentally exposed secrets, such as API keys, authentication tokens, or credentials that should not be committed to version control.
- **Dependency Scanning** analyzes dependencies (eg. third-party libraries) for known vulnerabilities. Many security risks arise from external components, so this layer is essential.
- **Container Scanning (GitLab integrated Trivy)** scans Docker container images for vulnerabilities in the operating system, applications, and dependencies to ensure that the runtime environment is secure as well.

These scans are configured to trigger automatically whenever a developer commits code or opens a merge request. The resulting reports are immediately available to developers and security, allowing for timely fixes and oversight.

#### 2.1.2 Merge request policy and GitLab access control
To further ensure quality and reduce the risk of unauthorized or flawed changes reaching production, our project enforces a mandatory peer review policy: no merge request can be accepted by its author alone. Each change must be reviewed and approved by at least one other team member before it can be merged into the main branch. This promotes accountability, code quality, and early detection of potential issues.

In our case, most GitLab repositories related to the project and thus the CI/CD-pipeline are publicly readable, but only authenticated GitLab users who are members of the project can modify them. This ensures transparency while maintaining controlled write access.

### 2.2 Environment Separation

Failure to properly segregate development, test, and production environments may result in loss of availability, confidentiality, and integrity of information assets. Such segregation is essential to prevent unauthorized or unintentional changes from affecting live systems, to reduce the risk of introducing vulnerabilities during testing or development, and to ensure that sensitive production data is not exposed to non-production environments. This control supports the principle of least privilege and promotes a secure software development lifecycle.

Our environment separation is based on a dual-VM architecture: one virtual machine is dedicated exclusively to production, while the other functions as a shared staging environment. The staging VM is configured to closely replicate the production setup, enabling realistic and reliable testing before deployment.

In line with the principle of least privilege, only the operations/admin role and the team leader have full access to the production environment. Other team members may be granted limited, temporary access when justified by operational needs.

Additionally, individual developers have access to their own private virtual machine instances, which can be used for initial development and isolated testing. This approach allows developers to experiment, debug, and validate features independently before pushing changes to the shared staging environment, where features undergo team-level testing and validation.

This setup ensures a clear separation between production and non-production environments, while still providing flexible and secure support for iterative development workflows.

---

## 3. Architecture-Level Security
### 3.1 Infrastructure Hosting: CSC Pouta Security
Our infrastructure is hosted on CSC’s Pouta cloud service, which provides a secure foundation for virtual machine deployment. The design of our architecture follows both CSC’s established security guidelines and our own internal best practices, ensuring protection at the network, system, and user levels.

Connectivity to the virtual machines is limited to SSH. CSC Pouta enforces firewall-level network restrictions via configurable Security Groups. In line with the principle of least privilege, we configure these rules to expose only the necessary ports to the public internet (eg. HTTPS (443) and SSH (22)). No unnecessary services, such as email servers, are installed on our instances unless they are explicitly required for the system's functionality.

At the system level, our SSH policy is build on Pouta’s security guidelines and default settings. The root user account is fully disabled for SSH access and has no password assigned. A separate administrative user account is available for system management tasks; it is configured to allow access only via a protected SSH key, never by password. This prevents brute-force password attacks, as only key-based authentication is accepted. All SSH keys are required to be protected with a strong passphrase to ensure they cannot be misused if compromised.

Additional user accounts, when needed, are limited to running a single service and are configured to block all local and remote logins. This aligns with Pouta’s security guidance and helps reduce the system's attack surface.

This security architecture ensures that only necessary services are exposed, that SSH access is restricted to authorized users with securely managed keys, and that user permissions are tightly scoped. Together, these measures help maintain high standards of confidentiality, integrity, and availability in both our production and testing environments.

### 3.2 Virtual machines (VM)
The virtual machines run Ubuntu 22.04 LTS, a long-term support version of the Linux operating system that benefits from regular security updates and a stable kernel. Ubuntu 22.04 includes built-in security features such as AppArmor, which enforces mandatory access control policies to confine processes and limit potential damage from compromised applications. The system also supports automatic security updates for critical packages via the unattended-upgrades service. Ubuntu 22.04 LTS has a lot of built in security features that increase the overall security of our infrastructure, but are out of scope for this document (eg. solution to Spectre vulnerability). For  a more comprehensive overview, follow [this](https://ubuntu.com/blog/whats-new-in-security-for-ubuntu-22-04-lts) link.

To further enhance security, Fail2Ban is installed on the virtual machines. This tool monitors system log files for patterns indicative of brute-force login attempts or other suspicious activity. Based on preconfigured filters and regular expressions, Fail2Ban can automatically block malicious IP addresses by modifying firewall rules. In our setup, it is also used to protect containerized services by watching relevant volumes for unauthorized access attempts. For more details, see [4.1.2 Fail2Ban](#412-fail2ban).

Although the Uncomplicated Firewall (ufw) is available on the system, it is currently inactive. Instead, network-level access control is enforced through Docker container configurations and CSC Pouta's external security groups, which define allowed ports and source IP ranges at the infrastructure level.

### 3.3 Other
- **Application Stack**: PrestaShop + Apache2 + MariaDB, containerized with Docker
- **Isolation**: Each core component runs in its own container
- **Network Restrictions**: Only essential ports are exposed (e.g. HTTPS 443)
- **Admin Access Path**: Custom path (not default) for PrestaShop back office

---

## 4. Server-Level Hardening
### 4.1 Implemented Server Hardening
#### 4.1.1 Apache2 is configured to use SSL/TLS encryption via Let's Encrypt
To protect communication between a web service and its users, the connection must be encrypted using either SSL (Secure Sockets Layer) or TLS (Transport Layer Security). This encryption is enabled through the use of digital certificates, which function like identity cards for servers. A valid certificate ensures that:

- The client is indeed talking to the intended server (not an imposter),
- The information transmitted cannot be intercepted or altered in transit.

Without encryption (i.e., when using plain HTTP), all data travels across the internet in cleartext. Anyone monitoring the traffic could read or tamper with it. This includes sensitive information like passwords, personal data, or payment details.

Let’s Encrypt is a free, automated, and open Certificate Authority (CA) that issues SSL/TLS certificates. The process of obtaining and renewing certificates is automated via the ACME protocol (Automatic Certificate Management Environment), which defines secure communication between clients and the CA.

In many hosting environments, the ACME client is provided and managed by the hosting provider. In our case, we maintain our own server, so we handle the certificate process ourselves.

We use Certbot, the most widely recommended ACME client, to obtain and manage SSL/TLS certificates. It runs directly on the server and requests the necessary certificate from Let’s Encrypt. Once issued, the certificate is installed on the web server (e.g., Apache), after which HTTPS connections are enabled.

> ⚠️ **Important!** Let’s Encrypt certificates are valid for 90 days. To maintain secure communication, certificates must be renewed regularly.

Certification renewal can be automated. To check if automatic renewal is configured:

```bash
sudo certbot renew --dry-run
```
or

```bash
systemctl list-timers | grep certbot
```
To renew the certificate manually (if needed):
```bash
sudo certbot renew
```

#### 4.1.2 Fail2Ban
Fail2Ban is a log-parsing intrusion prevention tool that helps secure your server against brute-force attacks and other suspicious activity. It monitors server logs in real time and reacts to patterns that indicate repeated failed access attempts or malicious behavior. In our architecture, Fail2Ban is installed to the VM. It has access to the relevant logs in the containers through volumes.

Fail2Ban uses filters tailored to specific services (e.g. SSH, Apache, Postfix), each defined by regular expressions that detect failed authentication attempts or unusual patterns in log entries. When a log line matches the filter’s `failregex` variable, Fail2Ban triggers a predefined action.

The most common (and default) action is to ban the offending IP address by modifying the system’s firewall rules, such as those set by `iptables` or `ufw`. Additional actions, such as sending alert emails to administrators, can also be configured.

Fail2Ban's behavior is controlled by settings such as:
- **Ban Time**: how long an IP remains blocked. Ccurrent setting is 600s (10 minutes).
- **Find Time**: how far back Fail2Ban looks for repeated failures. This is configured to 600s (10 minutes).
- **Max Retry**: number of allowed failures within the find time before triggering a ban. Current setting is 5 attempts.

These settings can be adjusted per service to suit your security needs. As it is, we chose to go with the default settings. To change the settings, first copy jail.conf file to jail.local and edit the latter with (eg.) nano.
```bash
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
sudo nano /etc/fail2ban jail.local
```

> ⚠️ **Important**: While it's possible to configure Fail2Ban by editing the jail.conf file itself, always copy the default jail.conf file to jail.local before making changes. Edits should be made in jail.local to avoid overwriting during package updates.

You can access Fail2Ban log files for example with the following command while in the VM environment:

```bash
sudo nano /var/logs/fail2ban.log
```

#### 4.1.3 Firewall Rules
Allowing essential movement only.

### 4.2 Server-Level features under consideration 
- **ModSecurity** Web Application Firewall will be installed with OWASP CRS rules
- **Containers** are run using non-root users (set in Dockerfile and Compose)
---

## 5. Application-Level Protection

### 5.1 Installed Security Modules

#### 5.1.1 PrestaScan (free version) – vulnerability and configuration scanner
PrestaScan installation process involves uploading a ZIP file, after which PrestaShop’s back office handles the installation automatically.

To activate the module, registration is required (as a merchant or agent). Once registered, scanning is initiated from:  
**Modules > PrestaScan > Configure > Start Scan**

The **free version** allows **one scan per week**. It provides the following core features:

- Scans installed modules for known vulnerabilities and update needs
- Identifies unused modules and allows bulk removal or disabling
- Alerts when a new vulnerability is discovered (including in back office modules)
- Lists known vulnerabilities in the current PrestaShop version
- Detects unprotected directories
- Sends email alerts about new vulnerabilities (after the first scan is run)

> **Note:** PrestaScan does *not* scan for malware. Future versions are planned to include this feature.

You can access the PrestaScan security reports from **Modules > PrestaScan > Configure**.

To access additional features like automated scans and weekly reports, a **Premium subscription** is required.

#### 5.1.2 Simple Security – IP blocking, logging, protection against brute-force attacks 

Simple Security provides protection against spam, bots, and brute-force attacks in PrestaShop. It helps secure the registration, login, contact, and newsletter forms, as well as modules like productcomments and iqitreviews. The module limits the number of login and registration attempts, detects and blocks over 90% of simple bots, and allows manual blocking or exclusion of specific IP or email addresses. It also logs login attempts and submitted form data for review.

To implement Simple Security you need to download Simple Security ZIP-file from PrestaShop forums. Note! When installing from the official ZIP-file, the module requires a manual edit to ensure compatibility with PrestaShop 1.7.8.0. In `simplesecurity.php`, line 105 should be changed to:

```php
$this->ps_versions_compliancy = ['min' => '1.7.8.0', 'max' => _PS_VERSION_];
```

After the modification you can implement the module through the PrestaShop back office.

> **Note:** The developer has confirmed testing Simple Security with PrestaShop version 1.7.8.3. Although the stated minimum supported version is 1.7.7, the developer has not tested the module with PrestaShop versions under 1.7.8.3.

After installation, the module adds two new sections under the Customers tab in the back office. "SS Triggers" allows defining phrases that will block spammy submissions from forms. Note, that the triggers only work on reviews left by users that have not registered, if you allow reviews from guests. Registered users will still be able to leave spammy reviews.

"SS Actions" provides a log of login attempts with options to view, edit, or delete entries. Configuration settings are available via the Module Manager, including thresholds for login attempts and form-based spam triggers.

We have configured Simple Security to warn users after 4 failed attempts and ban their ip-address after 7 for all forms. You can se individual amount of attempts for different forms if necessary (eg. bots targetyour "order news letter" form more than other forms, or customers are getting too easily banned while trying to login).  The interval during which the check is performed is set to 5 minutes.

#### 5.1.3 eiCAPTCHA / Google reCAPTCHA v2 – bot protection for forms

To protect the service from automated abuse and bot traffic, the `eicaptcha` module has been installed and configured. This module integrates Google's reCAPTCHA service into the platform.

To install eiCAPTCHA download the official ZIP-file from the developers web bage. After installing the `eicaptcha` module through PrestaShop backoffice modules:

1. Navigate to **Modules** → **Notifications** in the top menu.
2. Choose the appropriate settings for your use case.

We have configured the module to use **reCAPTCHA v2 check box**, which prompts users to manually verify they are human via check box. 

> ⚠️ **Important:** reCAPTCHA v3 is also available. It analyzes user behavior in the background and typically does not require user interaction. This provides a smoother user experience while still offering protection against bots. Nonetheless, we would advise against using v3, as there are serious questions about its compliance with GDPR.

To activate reCAPTCHA, you also need to obtain API keys from Google:

- Visit: [Google reCAPTCHA page](https://cloud.google.com/security/products/recaptcha?hl=fi) and scroll down to **"Get started for free"** to use the free version.

> **Note:** Google offers both free and paid versions of reCAPTCHA. Our production version uses the free version. Ensure you select the appropriate option based on your needs.

After registering your site with Google reCAPTCHA it is possible to set email alerts for supicious increase in your site activity and study reCAPTCHA event logs through their admin control panel: www.google.com/recaptcha/admin.

When reCAPTCHA v2 is active, forms of the website should have reCAPTCHA check boxes where the user can state, that they are human.

### 5.2 Planned Security Modules

#### 5.2.1 PrestaShop Official GDPR Module – data privacy management for end-users
The GDPR Compliance module is designed to support online store operators in aligning their operations with the General Data Protection Regulation (GDPR). While the module provides tools and guidance, the ultimate responsibility for compliance remains with the store owner.

The module helps address key GDPR requirements, including:  
1) The customer's right to access and transfer their personal data.  
2) The right to rectify or delete their personal information.  
3) The right to give or withdraw consent for data processing.

In addition to these features, the module offers guidance for PrestaShop users on GDPR-related matters. Under the first tab, users can view a list of all installed modules that collect customer data and are compatible with GDPR. If a module collects data but is not listed here, it is recommended to review its data handling practices and consider disabling it if necessary.

This tab also allows searching for customer-specific data, which can be exported (PDF or CSV) or deleted upon request. **Important:** Before deleting any data, make sure to save all receipts and transaction-related records that do not contain personally identifiable information.

Through the Consent Customization tab, users can edit the message shown in consent checkboxes across various forms. These checkboxes can be enabled in two places:  
1) In the account creation settings.  
2) In the customer information section.

It is recommended to create a dedicated page explaining data processing practices and link to it directly from the consent message.

The Customer Activity tab provides a summary of actions related to the customer's personal data, such as deletion requests. Finally, the module includes a Help tab with frequently asked questions and expert answers to support GDPR compliance efforts.

You can download the official ZIP-file from the developers webpage and install the module through PrestaShop back office.

---

## 6. User Data & Privacy (GDPR)

User data protection and privacy concerns are planned to be managed by the official Presta Shop GDPR module. We have not yet implemented this module.
- GDPR module supports:
  - Data export (PDF/CSV)
  - Data removal requests
  - Consent management
- Modules that collect personal data are automatically listed
- Consent messages are customizable for various forms
- A dedicated privacy policy page is linked directly in consent messages

---

## 7. Authentication & Access Control

- Admin panel URL is customized and not guessable
- Strong password policies are enforced
- Optional 2FA via third-party modules
- User activity logs available through Simple Security module

---

## 8. Additional Recommendations

- Regularly update PrestaShop core and all installed modules
- Monitor official PrestaShop security advisories
- Perform periodic vulnerability scans (internal and external)
- Backups should be encrypted and tested regularly

---

## 9. Contact

For questions or to report a security issue, please contact the security team via:

`ah0985@student.jamk.fi`
