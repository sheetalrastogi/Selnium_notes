<img width="667" height="362" alt="image" src="https://github.com/user-attachments/assets/601eea1f-0588-4f86-8768-446bb7f13eec" />

This slide describes the SOC Run & Maintain Phase, which focuses on operating, managing, improving, and optimizing a Security Operations Center after it has been established.

SOC Run & Maintain Lifecycle
SOC Operations
      ↓
Security Incident Monitoring & Handling
      ↓
Emergency Response Planning
      ↓
Forensics
      ↓
Asset Onboarding
      ↓
Optimization & Automation

1. SOC Operations / Service Level Management (SLM)

This area establishes how the SOC is governed and measured.

Activities
Define SLAs and KPIs

Examples:

Mean Time to Detect (MTTD)
Mean Time to Respond (MTTR)
Percentage of incidents resolved within SLA
Alert triage time
Create Process Checklists / Runbooks

Document standard procedures for:

Malware incidents
Phishing attacks
Unauthorized access
Data breaches
CAB Formation

CAB = Change Advisory Board

Responsible for reviewing:

Firewall rule changes
Security tool upgrades
Infrastructure changes
SIEM Administration

Manage tools like:

Microsoft Sentinel
Splunk
QRadar

Activities:

User management
Log source onboarding
Rule management
Storage monitoring
Governance Meetings

Conduct:

Monthly service reviews
Incident reviews
Risk reviews
Reporting

Prepare:

Daily SOC report
Weekly incident summary
Monthly executive dashboard
Deliverables
Contractual SLA Document
Service Management Plan (SMP)
2. Security Incident Monitoring & Handling

This is the day-to-day operational core of a SOC.

Activities
ITIL-Based Processes

The slide references:

Incident Management

Handle security incidents quickly.

Examples:

Malware detection
Suspicious login
Data leakage
Problem Management

Identify root causes.

Example:

Repeated phishing incidents due to weak email security.
Change Management

Control security-related changes.

Example:

Deploying a new EDR policy.
Service Level Management

Track compliance against agreed SLAs.

Risk Management

Assess business impact and likelihood.

Create SMP Aligned to SOW
SMP = Service Management Plan
SOW = Statement of Work

Ensures SOC operations match contractual obligations.

Identify Security Incidents

Examples:

Security Event	IncidentFailed login attempts	Brute-force attack
Large data transfer	Possible exfiltration
Malware alert	Compromised endpoint
Privilege escalation	Insider threat
Risk Mitigation

Determine:

Severity
Impact
Likelihood
Business exposure
Contain and Resolve

Example response process:

Alert
 ↓
Triage
 ↓
Investigate
 ↓
Contain
 ↓
Eradicate
 ↓
Recover
 ↓
Close

Retrospective Reviews

Conduct:

Root Cause Analysis (RCA)
Lessons Learned sessions
Process improvement reviews
Deliverables
Service Management Plan
SOC Transformation Plan
3. Emergency Response Planning

Focused on handling major cybersecurity incidents.

Activities
Build Emergency Response Team (ERT)

Typical members:

Team Member	ResponsibilitySOC Analyst	Detection
Incident Responder	Containment
Security Architect	Technical guidance
Legal Team	Regulatory response
Compliance Team	Regulatory reporting
PR Team	External communication
Investigate and Respond

Handle:

Ransomware
Data breach
Critical vulnerability exploitation
Insider threats
Compliance Adherence

Follow standards such as:

ISO 27001
NIST
PCI-DSS
GDPR
HIPAA
Management Updates

Provide:

Incident status
Impact assessment
Recovery progress
Effective Remediation

Examples:

Block malicious IPs
Patch vulnerabilities
Reset credentials
Update security controls
Deliverables
Operational Incident Reports
4. Digital Forensics

Forensics determines:

What happened, how it happened, when it happened, and who was affected.

Activities
Build Forensics Capability

Deploy tools for:

Disk forensics
Memory analysis
Log analysis
Network analysis

Examples:

EnCase
FTK
Volatility
X-Ways
Define Investigation Methodology

Evidence lifecycle:

Collection
 ↓
Preservation
 ↓
Analysis
 ↓
Reporting

Fraud & Breach Investigation

Examples:

Insider fraud
Credential theft
Data exfiltration
Financial fraud
Management Reporting

Provide:

Investigation status
Findings
Impact summary
Evidence Documentation

Maintain:

Chain of custody
Forensic artifacts
Screenshots
Packet captures
Audit logs
Deliverables
Forensic Investigation Report
5. Asset Onboarding

A SOC can only monitor assets that are onboarded.

Activities
Define Monitoring Scope

Assets:

Applications
Databases
Servers
Cloud workloads
Containers
Network devices
Enable Monitoring

Collect:

Logs
Events
Alerts

Perform:

Correlation
Alerting
Detection

Example:

Firewall Logs
      +
AD Logs
      +
Endpoint Logs
      ↓
SIEM Correlation
      ↓
Security Alert

Deliverables
Asset Inventory
Monitoring Configuration
CMDB / Service Management Records
6. Optimize (Continuous Improvement)

This is the SOC maturity and automation stage.

Activities
Process Automation

Identify repetitive tasks.

Examples:

Password compromise response
Malware containment
Ticket creation
Alert enrichment
Repeatable Workflows

Implement SOAR playbooks:

Phishing Alert
      ↓
Extract IOC
      ↓
Check Threat Intelligence
      ↓
Block Sender
      ↓
Create Ticket
      ↓
Notify User

Technology Optimization
Auto-Discover Endpoints

Detect:

New servers
Devices
Applications
Add Context to Incidents

Enrich alerts using:

Threat intelligence
Vulnerability data
User behavior data
Data Aggregation

Combine:

Network logs
Endpoint logs
Cloud logs
Application logs
Threat Intelligence

Leverage:

Indicators of Compromise (IOCs)
MITRE ATT&CK mappings
Threat feeds
Deliverables
SOC Automation Plan
Optimization Roadmap
Key Deliverables Across the Entire SOC Run & Maintain Phase
Area	DeliverableSOC Operations	SLA Guidelines
Incident Handling	Service Management Plan
Emergency Response	Operational Reports
Forensics	Investigation Reports
Asset Onboarding	Asset Inventory
Optimization	Automation Roadmap
Simple Explanation

The slide describes how a SOC operates after deployment:

Run daily monitoring and incident management
Respond to cyber attacks and emergencies
Perform forensic investigations
Onboard new applications, servers, and databases
Measure performance through SLAs and KPIs
Continuously improve through automation, threat intelligence, and process optimization

The ultimate goal is to move from reactive security monitoring to a mature, automated, intelligence-driven SOC that can detect, respond, investigate, and continuously improve cybersecurity operations.
