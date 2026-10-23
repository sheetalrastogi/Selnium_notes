<img width="652" height="207" alt="image" src="https://github.com/user-attachments/assets/ed5a05b1-7c63-4101-a5f8-4991991f03f6" />

The slide references several industry-recognized SOC best-practice frameworks and guidance documents. These are not compliance standards themselves, but they are commonly used to design, mature, and benchmark Security Operations Centers.

1. SANS - Building a SOC

Organization: SANS Institute

What It Is

SANS provides practical guidance for:

Creating a SOC from scratch
Defining SOC roles
Building analyst teams
Selecting tools
Creating monitoring processes
Defining maturity levels
Key Concepts
SOC Functions
Monitor
    ↓
Detect
    ↓
Investigate
    ↓
Respond
    ↓
Improve

SOC Roles
Role	ResponsibilitiesL1 Analyst	Alert Monitoring
L2 Analyst	Investigation
L3 Analyst	Threat Hunting
SOC Manager	Governance
Incident Responder	Remediation
Best Practices

✅ 24×7 monitoring

✅ Defined escalation paths

✅ Incident response playbooks

✅ KPI/SLA measurement

✅ Continuous threat hunting

Why Important

SANS is considered one of the most practical references for establishing and maturing a SOC.

2. Building a SOC on a Budget (AlienVault / OSSIM)
Purpose

Designed for organizations with:

Limited budgets
Small security teams
Initial SOC deployment requirements
Philosophy

Start small and mature gradually.

Recommended Approach
Phase 1
Log Collection
+
Centralized Monitoring
+
Basic Alerts

Phase 2
Threat Intelligence
+
Incident Response
+
Vulnerability Management

Phase 3
Automation
+
Machine Learning
+
Threat Hunting

Focus Areas
Open-source tools
Cloud-based tools
Managed SOC services
Risk-based implementation
Practical Lesson

Don't buy every security tool immediately.

Start with:

SIEM
Ticketing
Endpoint security
Vulnerability management

Then scale.

3. NIST SOC Concepts

Organization: National Institute of Standards and Technology (NIST)

NIST provides one of the most widely adopted cybersecurity frameworks worldwide.

NIST Cybersecurity Framework (CSF)

SOC activities map directly to the NIST functions:

NIST Function	SOC ActivitiesIdentify	Asset Discovery, Risk Assessment
Protect	Access Control, Security Controls
Detect	Monitoring, SIEM, Threat Detection
Respond	Incident Response
Recover	Business Recovery
NIST Security Lifecycle
Identify
    ↓
Protect
    ↓
Detect
    ↓
Respond
    ↓
Recover

NIST Incident Response Framework

SOC incident handling should follow:

Preparation
Tools
Processes
Training
Detection & Analysis
Monitor alerts
Analyze events
Validate incidents
Containment
Isolate affected systems
Eradication
Remove malware
Close vulnerabilities
Recovery
Restore services
Lessons Learned
Improve controls
Update playbooks
Prepare
   ↓
Detect
   ↓
Contain
   ↓
Eradicate
   ↓
Recover
   ↓
Lessons Learned

4. What is a SOC (McAfee)
Focus

Defines essential SOC capabilities and operating model.

Core SOC Pillars
People

SOC Analysts

L1
L2
L3
Threat Hunters
Process

Documented procedures:

Incident Response
Escalation
Threat Intelligence
Reporting
Technology

Tools supporting:

SIEM
SOAR
EDR
Threat Intelligence
Related Standards Commonly Used with SOC

Although not shown explicitly on this slide, mature SOC implementations usually align with the following standards.

ISO 27001
Purpose

Information Security Management System (ISMS)

SOC Relevance

Controls related to:

Incident management
Access control
Monitoring
Logging
Risk management
Example Controls
A.5 Organizational Controls
A.8 Technology Controls

NIST 800-61
Purpose

Computer Security Incident Handling Guide

SOC Usage

Incident response procedures.

Covers:

Detection
Analysis
Containment
Eradication
Recovery
NIST 800-53
Purpose

Security and Privacy Controls Framework

SOC Controls

Examples:

AU = Audit and Logging
IR = Incident Response
SI = System Integrity
AC = Access Control
MITRE ATT&CK
Purpose

Adversary behavior framework.

SOC Usage

Map attacks to techniques.

Example:

Attack	ATT&CK TechniquePhishing	T1566
Credential Theft	T1003
Lateral Movement	T1021

SOC analysts use ATT&CK to:

Create use cases
Build detections
Perform threat hunting
ITIL
Purpose

IT Service Management Framework

SOC Usage

Processes for:

Incident Management
Problem Management
Change Management
Service Level Management

These were referenced in the earlier "Run & Maintain" slide.

SOC Maturity Model

A mature SOC generally evolves through the following stages:

Level	CharacteristicsLevel 1	Basic Log Monitoring
Level 2	SIEM & Alerting
Level 3	Incident Response
Level 4	Threat Intelligence
Level 5	Threat Hunting
Level 6	SOAR Automation
Level 7	AI-driven SOC
Interview / Assessment Summary

When asked "Which standards and frameworks are typically used for a SOC?", a strong answer is:

NIST CSF for cybersecurity governance.
NIST 800-61 for incident response.
NIST 800-53 for security controls.
ISO 27001 for information security management.
MITRE ATT&CK for threat detection and hunting.
ITIL for SOC service management.
SANS SOC Framework for SOC design and operations.

Together, these frameworks provide guidance for People, Process, Technology, Governance, Incident Response, Threat Intelligence, Compliance, and Continuous Improvement, which are the core pillars of a modern Security Operations Center.
