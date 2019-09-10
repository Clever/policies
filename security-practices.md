# Clever Security Practices
* [Overview](#overview)
* [Product security](#product-security)
  * [Secure Software Development Lifecycle](#secure-software-development-lifecycle)
  * [Security Features](#security-features)
* [Infrastructure security](#infrastructure-security)
  * [Third-Party Vulnerability Management](#third-party-vulnerability-management)
  * [Vulnerability Scanning](#vulnerability-scanning)
  * [Change Management](#change-management)
  * [Availability and Disaster Recovery](#availability-and-disaster-recovery)
  * [Data Encryption in Storage and Transit](#data-encryption-in-storage-and-transit)
  * [Data Isolation](#data-isolation)
  * [Network Isolation](#network-isolation)
  * [Logging](#logging)
  * [Threat Detection](#threat-detection)
  * [Secret Storage](#secret-storage)
  * [Patching](#patching)
* [IT security](#it-security)
  * [Policies and Standards](#policies-and-standards)
  * [Device Policies](#device-policies)
  * [Account Policies](#account-policies)
  * [Security Training](#security-training)
  * [Third-Party Software](#third-party-software)
  * [Background Checks](#background-checks)
  * [Cyber Insurance](#cyber-insurance)
* [Other Security Practices](#other-security-practices)
  * [External Security Assessment](#external-security-assessment)
  * [Incident Management and Response](#incident-management-and-response)
## Overview
Clever&rsquo;s mission of enabling education technology in the classroom depends on the security of our systems. We want our customers - application administrators, district administrators, teachers, and students - to know that Clever is a trustworthy guardian of sensitive data.
Our [Privacy Policy](privacy-policy.md) and [Terms of Use](general-terms-of-use.md) describe Clever&rsquo;s data practices, and this document details our information security program. Principles of an effective security program include being threat-driven, using automation to scale, and balancing the investment between prevention and response.

Our program has three focus areas: product security, infrastructure security, and IT security. The following sections describe each focus area and the set of security activities we practice within each.
## Product security
The goal of Clever&rsquo;s product security efforts is to clarify the security and privacy impact of new features and products as they are being created to let Clever engineering continuously improve the Clever product safely.
### Secure Software Development Lifecycle
We have an application security review process that applies to all new development projects. It includes threat modeling and code review. Security design reviews occur for any major change. We have a secure code review process that identifies high-risk code for manual review by security experts. We use automation in our software development build pipeline that analyzes code for potential vulnerabilities.
Our knowledge management portal includes application security training material with secure coding guidelines specific to our technology stack, which all new engineering hires review. These coding guidelines include discussion of OWASP Top Ten issues like SQL injection, Cross-Site Scripting (XSS), and Cross-Site Request Forgery.
We have an active bug bounty program that rewards external security researchers for reporting vulnerabilities in Clever to us. We&rsquo;re responsive to security inquiries sent to security@clever.com.
### Security Features
Clever shares data at the discretion of districts, meaning vendors only get access to a district&rsquo;s data when authorized by the district. Vendors syncing data from Clever have agreed to store, transmit, and display student data only via secure and FERPA compliant methods. Districts can control, at granular levels, the student records that are shared.
Application and district administrators can invite users to their Clever accounts with limited permissions, using a role-based access control system.
Clever protects against password brute forcing by rate limiting login attempts. Clever salts and hashes passwords using bcrypt, a high-cost hashing function. Clever offers and recommends two-factor authentication administrator account access, requiring authorized team members to first log in using their email address and password, then enter a temporary six-digit code sent to their connected mobile device.
We use Content Security Policy (CSP) to detect and prevent unauthorized Javascript from running in the context of our applications.
You can read posts from our security team on our [engineering blog](https://engineering.clever.com/category/security/).
## Infrastructure security
Our infrastructure security efforts focus on accelerating the pace of our engineering teams by providing the underlying tools, systems, processes, and knowledge resources to build secure and privacy-protecting systems.
All of Clever&rsquo;s infrastructure runs in the cloud. Our primary cloud provider, AWS, conforms to security standards including SOC 1/SSAE 16/ISAE 3402, SOC 2, PCI DSS Level 1, ISO 27001, and FISMA. See https://aws.amazon.com/compliance/ for more details.
### Third-Party Vulnerability Management
We monitor security release information for software in our stack as well as global vulnerability feeds. When a vulnerability that affects is released, we prioritize the rollout of the patch based on the severity, or impact, of the vulnerability in question. Clever monitors vulnerability feeds including US-CERT Alerts and the National Vulnerability Database. This feed is supplemented in-house experts on various technologies who are each responsible for monitoring technology-specific concerns on message boards, security researcher discussion forums, and other sources for vulnerability information.

### Vulnerability Scanning
We use automated security scanning tools to notify us quickly of changes to or activities in our infrastructure that may result in a security issue. The results of these scans are regularly triaged by our security team.

### Change Management
We have a change management process for our infrastructure that includes source code control, peer code review, logging, and alerts for unusual behavior. All production changes are deployed with an automated system that detects reliability issues and reverts problematic deploys. Our automation allows us to safely and reliably deploy code to production dozens of times a day.
### Availability and Disaster Recovery
Our availability is 99.9% or higher - see https://status.clever.com for more details.
We have established a set of practices and tools to defend against automated Denial of Service (DoS) attacks against Clever&rsquo;s infrastructure.
Since our service is based entirely in the cloud, our disaster recovery plan is based on best practices from AWS for maintaining resiliency in the case of disaster. We use multiple AWS availability zones to safeguard against single data-center issues.
Clever generates data backups regularly and stores them securely with our cloud provider. Backups are stored as long as needed - in no case longer than 60 days - and deprovisioned securely by our cloud provider.
### Data Encryption in Storage and Transit
We encrypt all Personally Identifiable Information (PII) in transit outside of our private network and at rest in our private network. We use strong forms of cryptography like AES256-GCM with access-controlled keys that are regularly audited and rotated. Our TLS configuration gets an A+ from [ssllabs.com](https://www.ssllabs.com/ssltest/analyze.html?d%3Dclever.com%26latest), and we use HSTS to ensure that pages are loaded over HTTPS connections.
### Data Isolation
Clever uses logical separation to process data in a multi-tenant environment. The code controls are tested before every production deploy. Data processing occurs in containerized environments with limited access to external resources. Services use ephemeral credentials for services to access data stores. All data is stored in the USA.
### Network Isolation
Clever limits external access to network services by running them inside of a Virtual Private Cloud (VPC) and blocking all unnecessary ports from external traffic. Access to our production network is limited to necessary personnel, logged, and secured using multiple factor authentication. We use a bastion SSH host to gate all system-level access to production infrastructure.
### Logging
Clever maintains a centralized log for product and infrastructure events and metrics. Tightly access-controlled and integrity protected log backups are persisted to access-controlled archival stores on S3. All system-level actions performed in production environments with elevated permissions (sudo) are logged.
### Threat Detection
We have monitoring, alerting, and response processes for suspicious activity occurring in our infrastructure.
### Secret Storage
No secret data (passphrases, API keys, QR Codes for 2-factor, etc) are sent using tools like Gmail, Dropbox or Slack. We have purpose-built tools for storing and transferring this data in accordance with our security requirements.
### Patching
We regularly update our operating systems images, container images, language runtimes, and language libraries to the latest known supported versions.
## IT security
The goal of our IT security practices is to make employees more productive by reducing the mental overhead of safely computing. The security team gives Clever employees the tools they need to do their job safely. The lines of communication between security and other parts of the company are always open, and the justification for decision making and advice is clear.
### Policies and Standards
Our information security policy is documented on our knowledge sharing portal. We have a Clever Data Classification standard that describes the different types of data that our employees work with and how that data should be handled.
### Device Policies
Our device policy describes best practices for device configuration and software usage. It mandates full disk encryption for all devices that have access to sensitive data, the use of screen locks after a period of inactivity, and remote wipe capabilities. It also describes our permitted software and software update practices.
### Account Policies
Our account policies states that all passwords should be securely stored and generated with a password manager, and mandates the use of 2FA for sensitive accounts. It also defines the OAuth authorization policies for accounts with sensitive data access (e.g. GSuite) and the techniques to avoid phishing.
Accounts are activated when an employee joins and deactivated when an employee leaves, using automated processes where possible.
### Security Training
We create a culture of security for all Clever employees through activities like security awareness training and awarding security-conscious behavior. Our security program that details each of these components is documented on our knowledge sharing portal. All new hires are required to read the information security policy and undergo information security training, and existing employees have regular refresher training.
### Third-Party Software
We have a third-party software security review process that must be completed before using new services at our organization. The level of verification varies based on the risk profile of the service in question.
### Background Checks
All Clever employees undergo criminal background checks and sign agreements barring any use of confidential information outside of the scope of their work with the company.
### Cyber Insurance
We cyber liability insurance with coverage of five million US dollars.
## Other Security Practices
### External Security Assessment
We conduct an annual external security assessment of our applications. We make the reports associated with these assessments available for our users, on request.
### Incident Management and Response
Clever has a standardized process for responding to security incidents. When a security incident is suspected, teams are notified through a paging service and a central communication channel is established. After each incident, we conduct a post-mortem analysis to identify root causes and track any related follow-up work.

If Clever believes that a customer&rsquo;s personal information has been accessed or modified by an unauthorized third party, we will take all necessary steps to notify the affected customers as quickly as possible, and in no case greater than two business days after we learn of the breach.

One of the first steps during a security incident is to verify that the attacker is completely out of the systems question, or that their impacts are minimized. The second step is to identify the extent of the data breach, which should result in a list of the affected customers and data. In the event of a large data breach, we will coordinate with additional legal and security resources to assist our efforts.

In our communications with affected customers, we will include the following information:
* - The nature of how the information was accessed (viewed, modified, etc)
* - The actual information accessed
* - What we&rsquo;ve done to mitigate the access
* - What corrective actions we will take to prevent future breaches
If you have any questions about Clever's security program, please send an email to security@clever.com.
