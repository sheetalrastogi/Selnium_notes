<img width="653" height="364" alt="image" src="https://github.com/user-attachments/assets/16f8c7da-e7fa-46a7-87b0-155662a560f5" />

This diagram shows a Security Operations Center (SOC) Operational Framework, which describes how a SOC aligns business security requirements with monitoring, detection, response, governance, and continuous improvement activities.

1. Business Requirements Layer (Top)

The SOC exists to support the organization's security and compliance objectives.

Key Drivers:

Security
Strategy
Policies & Standards
Risk Management
Compliance
Purpose

This layer defines:

What must be protected
Regulatory obligations
Risk appetite
Security goals
Service expectations

Examples:

ISO 27001 compliance
PCI-DSS requirements
GDPR compliance
Cybersecurity policies
Business continuity requirements
2. Security Intelligence Layer (Core SOC Functions)

This is the heart of the SOC where data is analyzed and security operations are performed.

A. Incident & Reporting

Responsible for:

Security incident tracking
Reporting security events
Metrics and dashboards
Executive reporting

Activities:

Ticket creation
Incident classification
Monthly SOC reports
KPI tracking
B. Security Analytics

Analyzes logs, alerts, and threat data.

Activities:

Threat Monitoring
Threat Analysis
Impact Analysis

Example:

Detect unusual login activity
Identify malware communication
Analyze attack patterns
C. Security Audits

Ensures security controls are functioning properly.

Activities:

Security assessments
Regulatory reviews
Configuration audits
Control effectiveness reviews
D. Emergency Response

Handles active cyber incidents.

Activities:

Investigation
Event Analysis
Escalation

Examples:

Ransomware attack
Data breach
Credential compromise
DDoS incident
E. Advisory Services

Provides security guidance to business and IT teams.

Examples:

Security recommendations
Architecture reviews
Vulnerability remediation guidance
Risk consultation
3. Operational Support Areas
Administration Support

Maintains SOC tools and infrastructure.

Activities:

Tool deployment
Tool integration
Tool administration

Examples:

SIEM maintenance
EDR deployment
Firewall integration
Threat Monitoring

Continuous monitoring for suspicious activities.

Activities:

Real-time alert review
Threat hunting
Threat intelligence correlation
Threat Response

Responds to identified threats.

Activities:

Investigation
Event analysis
Escalation

Output:

Containment
Eradication
Recovery
Operations Management

Day-to-day service management.

Activities:

Incident Management
Problem Management
Change Management
Service Level Management (SLM)
4. Client Infrastructure Layer

This is the source of security data.

Inputs Collected
Logs

Machine-generated records:

Server logs
Application logs
Firewall logs
Database logs
Alerts

Security notifications from tools:

Antivirus alerts
EDR detections
IDS/IPS alerts
SIEM alerts
Events

User and system activities:

User logins
File access
Configuration changes
Network activity

These feeds are ingested into the SOC for analysis.

5. SOC Operations & Governance (Vertical Layer)

This spans the entire framework.

Responsibilities
Governance
Policies
Processes
Roles & responsibilities
Compliance oversight
Operational Oversight
Performance management
Service quality
Escalation management
Continuous improvement

The SOC must operate according to defined governance standards.

6. Foundation Layers

These support the overall framework.

Governance

Defines:

Security policies
Standards
Procedures
Accountability

Examples:

ISO 27001
NIST CSF
CIS Controls
Potential Risks & Mitigation

Identifies:

Cyber threats
Vulnerabilities
Business risks

Mitigation Examples:

MFA implementation
Patching
Network segmentation
Security awareness training
Recommended Tools & Technologies

Typical SOC Technology Stack:

Function	ToolsSIEM	Splunk, QRadar, Sentinel
EDR	CrowdStrike, Defender, SentinelOne
SOAR	Palo Alto XSOAR, Splunk SOAR
Vulnerability Management	Tenable, Qualys, Rapid7
Threat Intelligence	MISP, Recorded Future
Ticketing	ServiceNow, Jira
Checkpoints

Periodic reviews to ensure effectiveness.

Examples:

SLA reviews
Audit reviews
Security posture assessments
Maturity assessments
KPI/KRI reviews
End-to-End SOC Workflow
Business Requirements
        ↓
Governance & Policies
        ↓
Infrastructure Generates Logs/Alerts/Events
        ↓
SOC Monitoring & Security Analytics
        ↓
Threat Detection
        ↓
Incident Investigation
        ↓
Response & Escalation
        ↓
Reporting & Compliance
        ↓
Continuous Improvement

SOC Service Catalogue Derived from This Framework
Security Monitoring (24x7)
Log Management
SIEM Operations
Threat Detection & Hunting
Incident Response
Malware Analysis
Vulnerability Management
Security Audits
Compliance Reporting
Change & Problem Management
Threat Intelligence
Security Advisory Services
Governance & Risk Management
Tool Administration & Support
SLA Monitoring & Reporting
In Simple Terms

The framework shows how a SOC takes logs, alerts, and events from the organization's infrastructure, uses security intelligence and analytics to detect threats, performs investigation and response, and reports outcomes back to the business while maintaining governance, compliance, risk management, and continuous improvement throughout the process.



