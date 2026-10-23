<img width="589" height="185" alt="image" src="https://github.com/user-attachments/assets/9f9c3e46-2f79-447a-81e7-54e47ef55807" />
This slide points to some industry best practices and guidance documents for Vulnerability Assessment (VA). These are reference frameworks that help organizations establish a mature vulnerability management program.

What is a Good VA Program?

A mature VA program should:

Discover Assets
      ↓
Scan Regularly
      ↓
Identify Vulnerabilities
      ↓
Prioritize Risks
      ↓
Remediate
      ↓
Validate Fixes
      ↓
Report Metrics
      ↓
Repeat


The references in the slide support this lifecycle.

1. 7 Best Practices for Vulnerability Assessment
1. Maintain an Accurate Asset Inventory

You cannot secure assets you don't know exist.

Track:

Servers
Databases
Applications
APIs
Cloud Resources
Endpoints
Example
Known Assets = 500 Servers

Actual Assets = 600 Servers

100 Servers Unmonitored


Risk: Hidden attack surface.

2. Define Assessment Scope Clearly

Before scanning:

What systems are included?
What systems are excluded?
Which environments are in scope?

Example:

✅ Production Web Servers
✅ APIs
✅ Databases

❌ Developer Laptops

3. Perform Regular Scanning

Recommended frequencies:

Asset Type	FrequencyInternet-facing systems	Weekly
Internal servers	Monthly
Critical applications	Monthly
Penetration Testing	Quarterly/Yearly
4. Use Authenticated Scans

Authenticated scans provide deeper visibility.

Without Authentication:

External View Only


With Authentication:

Patch Levels
Configurations
User Permissions
Installed Software

5. Risk-Based Prioritization

Don't fix vulnerabilities based solely on CVSS.

Consider:

Technical Severity
+
Business Impact
+
Exposure
+
Exploit Availability

Example
Vulnerability	CVSS	Business PriorityPayroll SQL Injection	8.5	Critical
Test Server Patch Missing	9.0	Medium
6. Verify Remediation

Never assume patches solved the issue.

Perform:

Fix Applied
      ↓
Re-Scan
      ↓
Verify Closure

7. Measure and Report

Track KPIs such as:

Open vulnerabilities
Closed vulnerabilities
MTTR (Mean Time to Remediate)
SLA compliance

Example:

Critical Findings : 20
Resolved : 18
Remaining : 2

2. VA - ISACA Best Practices

ISACA focuses on governance, risk, and compliance.

Key Recommendations
Risk-Based Approach

Assess vulnerabilities based on:

Business impact
Regulatory impact
Data sensitivity
Governance

Define:

Roles
Responsibilities
Ownership

Example:

Role	ResponsibilitySecurity Team	Identify vulnerabilities
Application Team	Fix vulnerabilities
Management	Accept residual risk
Continuous Monitoring

VA should not be annual-only.

Recommended:

Continuous Scanning
Continuous Monitoring
Continuous Improvement

Documentation

Maintain:

Scan reports
Risk registers
Closure evidence
Exception approvals
3. Vulnerability Management - US-CERT

US-CERT (United States Computer Emergency Readiness Team) promotes a structured vulnerability management lifecycle.

US-CERT Vulnerability Lifecycle
Discover
    ↓
Evaluate
    ↓
Prioritize
    ↓
Remediate
    ↓
Verify

Key Practices
Asset Discovery

Identify all devices connected to the environment.

Examples:

Servers
Applications
Containers
Cloud Resources
Network Devices

Vulnerability Assessment

Use tools like:

Nessus
Qualys
OpenVAS

to identify weaknesses.

Prioritization

Focus on:

Critical systems
Internet-facing systems
Exploitable vulnerabilities
Remediation

Options include:

Patch
Upgrade
Configuration Change
Compensating Controls

Validation

Confirm fixes through:

Re-scan
Re-test
Manual Validation
4. Vulnerability Management - BeyondTrust

BeyondTrust emphasizes practical vulnerability management rather than simply generating scan reports.

Key Principles
Vulnerabilities Without Context Create Noise

Large organizations may see:

50,000+ vulnerabilities


Not all require immediate action.

Prioritize According to Exposure

High Priority:

✅ Internet-facing assets

✅ Critical business systems

✅ Public exploits available

Low Priority:

❌ Isolated test systems

❌ Decommissioned systems

Integrate With Patch Management

Example:

Scan
   ↓
Find Missing Patch
   ↓
Create Ticket
   ↓
Deploy Patch
   ↓
Verify Fix

Reduce Mean Time To Remediate (MTTR)

Measure:

Discovery Date
         ↓
Remediation Date


Organizations should continuously reduce remediation time.

Continuous Improvement

Each scan cycle should improve:

Security posture
Compliance
Risk visibility
Best-Practice VA Governance Checklist

Before declaring a VA program mature, verify:

Process
✅ Defined Vulnerability Management Process
✅ Documented Standards
Scope
✅ Asset Inventory Exists
✅ Scope Approved
Execution
✅ Regular Scans Performed
✅ Authenticated Scans Used
✅ False Positives Reviewed
Risk Management
✅ Risk-Based Prioritization
✅ Vulnerability Database Maintained
Remediation
✅ Owners Assigned
✅ SLA Defined
✅ Closure Verified
Reporting
✅ Executive Reports
✅ Technical Reports
✅ Risk Dashboard
Interview/Assessment Summary

A strong answer to "What are the best practices for Vulnerability Assessment?" is:

Maintain a complete asset inventory.
Define and approve assessment scope.
Follow recognized frameworks (OWASP, NIST, ISACA, CIS).
Perform regular authenticated vulnerability scans.
Prioritize findings based on business risk, not only severity scores.
Track remediation through ownership and SLAs.
Re-scan to validate fixes.
Continuously monitor and report security metrics.
Integrate VA with threat intelligence and patch management.
Maintain governance, compliance evidence, and executive reporting.

In short: Effective VA is not about finding the most vulnerabilities; it is about identifying the vulnerabilities that matter most to the business and ensuring they are remediated and verified.
