<img width="642" height="359" alt="image" src="https://github.com/user-attachments/assets/fbcdd918-a7b2-439d-a4ca-b44828f4a4cd" />
<img width="611" height="273" alt="image" src="https://github.com/user-attachments/assets/d14c628a-d9e3-435b-a697-9ea855f0e6c6" />

These slides focus on Cybersecurity Governance and Assessment Frameworks, which provide the management structure around SOC, VAPT, compliance, risk management, and security operations.

1. Best Practices / Frameworks

These are the standards against which organizations are assessed.

SOX (Sarbanes-Oxley Act)
Purpose

Financial reporting and internal controls.

Security Focus
Change management
Access controls
Audit trails
Data integrity
Typical Questions

✅ Who can modify financial systems?

✅ Is every change approved and tracked?

✅ Are logs retained?

CIS Controls
Purpose

Practical cybersecurity controls.

Examples
Asset Inventory
Vulnerability Management
Secure Configuration
Access Management
Security Monitoring
Benefits
Easy to implement
Prioritized controls
Good maturity framework
ISO 27001
Purpose

Information Security Management System (ISMS)

Focus Areas
Risk Management
Security Governance
Policies
Compliance
Security Operations
Deliverables
Security Policies
Risk Register
Risk Treatment Plan
Incident Response Process
OWASP
Purpose

Application Security Framework

Common Areas
SQL Injection
XSS
Broken Authentication
API Security
Used By
Development Teams
Security Teams
DevSecOps Teams
FFIEC
Purpose

Financial industry cybersecurity framework.

Used by:

Banks
Financial Institutions
Payment Organizations
Focus Areas
Online Banking Security
Fraud Prevention
Cyber Resilience
SOC I / SOC II / SOC III
SOC 1

Focuses on controls affecting financial reporting.

SOC 2

Focuses on:

Security
Availability
Confidentiality
Privacy

Most common for SaaS providers.

SOC 3

Public version of SOC 2.

HIPAA
Purpose

Healthcare data protection.

Protects
Patient Records
Medical Data
Healthcare Systems
PCI-DSS
Purpose

Payment Card Security.

Applies when handling:

Credit Cards
Debit Cards
Payment Information
Requirements
Encryption
Logging
Vulnerability Management
Access Controls
2. Governance Model

This slide explains how an organization governs cybersecurity operations.

A. Organization Structure
Purpose

Define who manages security operations.

Activities
Create Organization Chart

Example:

CISO
  │
SOC Manager
  │
├── L3 Analysts
├── L2 Analysts
└── L1 Analysts

Define RACI

RACI =

Term	MeaningR	Responsible
A	Accountable
C	Consulted
I	Informed

Example:

Activity	Security Team	IT TeamVulnerability Scan	R	C
Patch Deployment	C	R
Define Roles & Responsibilities

Examples:

SOC Manager
Security Architect
Incident Response Lead
Compliance Manager
Create Skill Matrix

Example:

Skill	Analyst A	Analyst BSplunk	Expert	Intermediate
Sentinel	Intermediate	Expert
Capacity Planning

Determine staffing requirements.

Example:

Day Shift = 4 Analysts
Night Shift = 3 Analysts

B. Communication Plan
Purpose

Ensure security communications are structured.

Activities
Stakeholder Identification

Example:

CISO
Operations Team
Compliance Team
Vendors
Review Meetings
Strategic Reviews

Monthly/Quarterly

Focus:

Risk
Maturity
Compliance
Tactical Reviews

Weekly

Focus:

Open Incidents
Vulnerabilities
Projects
Escalation Matrix

Example:

Critical Incident
      ↓
SOC Manager
      ↓
CISO
      ↓
Executive Committee

C. KPI Tracking & Reporting
Purpose

Measure effectiveness.

Examples of KPIs
SOC KPIs
MTTD (Mean Time to Detect)
MTTR (Mean Time to Respond)
VAPT KPIs
Open Vulnerabilities
Closed Vulnerabilities
Vulnerabilities by Severity
Security KPIs
Top 10 Attacks
False Positives vs True Positives
Incident Trends
Reporting Example
Critical Vulnerabilities: 10
Resolved: 8
Remaining: 2

D. Training Plan
Purpose

Ensure teams remain skilled.

Activities
Identify Training Needs

Examples:

SOC Analyst Training
SIEM Training
Cloud Security Training
VAPT Training
Create Skill Matrix

Before Training:

Splunk: Beginner


After Training:

Splunk: Advanced

Cross-Skilling

Example:

SOC Analyst
      ↓
Threat Hunter
      ↓
Incident Responder

E. Risk Management
Purpose

Identify and manage business risks.

Activities
Identify Risks

Sources:

VAPT Findings
Audits
Security Incidents
Compliance Reviews
Risk Categorization
Risk	ExampleStrategic	Lack of SOC
Operational	Weak Monitoring
Compliance	PCI Non-Compliance
Technical	Unpatched Servers
Risk Assessment

Formula:

Risk = Impact × Probability


Example:

Impact	Probability	ResultHigh	High	Critical
Mitigation Planning

Example:

Risk:
No MFA

Mitigation:
Implement Microsoft Entra MFA

F. Third-Party / Vendor Management
Purpose

Manage security risks from suppliers and vendors.

Activities
Create Agreements

Examples:

NDA
SLA
Security Clauses
Vendor Assessments

Questions:

Is vendor ISO 27001 certified?
Does vendor have SOC 2?
Does vendor use encryption?
Background Checks

For:

Vendor Staff
Managed Service Providers
Contractors
Resource Planning

Ensure:

Vendor availability
Backup resources
Escalation contacts
How the Governance Model Works Together
Organization Structure
          ↓
Communication Plan
          ↓
KPI Tracking
          ↓
Training Program
          ↓
Risk Management
          ↓
Vendor Management
          ↓
Continuous Improvement

Key Deliverables
Area	DeliverableOrganization	Org Chart, RACI Matrix
Communication	Communication Plan, Escalation Matrix
KPI Reporting	SOC Reports, VAPT Reports
Training	Skill Matrix, Training Plan
Risk Management	Risk Register, Risk Treatment Plan
Vendor Management	Vendor Tracker, SLA Register
Simple Summary

These slides explain how cybersecurity is governed at an organizational level. Technical controls such as SOC, SIEM, VAPT, and Incident Response are only effective when supported by:

Clear organizational structure
Defined responsibilities (RACI)
Communication and escalation plans
KPI measurement and reporting
Training and skill development
Risk management processes
Third-party/vendor governance

In short:

People
 + Process
 + Governance
 + Technology
 = Effective Cybersecurity Program
