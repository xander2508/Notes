- What exactly are we protecting?
- What are the most valuable assets the organization owns that need securing?
- What can be considered the perimeter of our network?
- What devices & services can be accessed from the Internet? (Public-facing)
- How can we detect & prevent when an attacker is attempting an attack?
- How can we make sure the right person &/or team receives alerts as soon as something isn't right?
- Who on our team is responsible for monitoring alerts and any actions our technical controls flag as potentially malicious?
- Do we have any external trusts with outside partners?
- What types of authentication mechanisms are we using?
- Do we require Out-of-Band (OOB) management for our infrastructure. If so, who has access permissions?
- Do we have a Disaster Recovery plan?

[Tactics - Enterprise | MITRE ATT&CK®](https://attack.mitre.org/tactics/enterprise/)

Penetration testers not only focus on identifying and exploiting vulnerabilities but also provide actionable recommendations to address these issues. Key mitigations and detections for common TTPs include:

- Physical hardware changes
- Network infrastructure modifications
- Host baseline adjustments

## Setting a Baseline

A robust understanding of the network environment enables quick identification of anomalies such as new hosts, tools, or unusual traffic. This requires regular audits (annually or more frequently) of the following:

### Items to Document and Track

- **DNS records, network device backups, DHCP configurations**
- **Application inventory**: Ensure all applications are logged and up-to-date.
- **Enterprise host inventory**: Include host locations and roles.
- **Users with elevated permissions**: Document and monitor privileged accounts.
- **Dual-homed hosts**: List systems with more than one network interface.
- **Visual network diagram**: Tools like Netbrain or diagrams.net can assist in creating interactive, up-to-date network schematics.

### Asset Monitoring and Critical Asset Identification

Identify and monitor assets critical to operations to prioritize security measures effectively.

---

## People, Processes, and Technology

### **People**

Human users are often the weakest link in security. Training and enforcing best practices mitigate risks such as phishing and poor password management.

#### Key Measures

- **Multi-Factor Authentication (MFA)**: Implement multiple authentication factors (e.g., something you know, have, or are).
- **BYOD Policies**: Establish security guidelines for personal devices to prevent risks like malware infections.
- **Security Operations Center (SOC)**: A SOC team ensures 24/7 monitoring, incident response, and operational security.

#### Example Scenario: BYOD Risks

Nick, a logistics manager using his infected personal laptop for work, introduces malware into his organization’s network. This highlights the critical need for BYOD security policies, segmented networks, and endpoint monitoring.

---

### **Processes**

Defined policies and procedures are critical for consistent security enforcement and incident response.

#### Key Processes

- **Asset Management**: Use tags and inventories to track hosts.
- **Access Control**: Implement user account provisioning/de-provisioning and MFA policies.
- **Change Management**: Document changes to identify accountability and streamline troubleshooting.
- **Host Provisioning/Decommissioning**: Utilize baseline hardening guidelines and gold images.

#### Disaster Recovery

Maintain and regularly test a disaster recovery plan to ensure readiness for breaches or system failures.

---

### **Technology**

Maintaining secure technology environments involves identifying and addressing misconfigurations, vulnerabilities, and emerging threats.

#### Perimeter Security

- **Identify valuable assets**: Secure the organization’s critical assets.
- **Detect and prevent attacks**: Use Next-Gen Firewalls (NGFWs), intrusion detection systems (IDS), and intrusion prevention systems (IPS).
- **Alerting and monitoring**: Ensure alerts are directed to responsible teams promptly.

#### External Perimeter Questions

- What services/devices are public-facing?
- How are alerts monitored, and by whom?
- Are external trusts and authentication mechanisms secure?
- Is Out-of-Band (OOB) management implemented?

#### Hybrid Infrastructure

Consider both on-premises and cloud environments when assessing and securing organizational infrastructure.

---

### Internal Considerations

Focus on internal security through network segmentation, host hardening, and monitoring. Key questions to ask include:

- Are internet-exposed hosts placed in a DMZ?
- Are different teams confined to network segments?
- Are production and management networks separated?
- Are approved remote-access users tracked?

#### Monitoring and Correlation

Implement tools like SIEM to analyze logs and correlate data across endpoints and infrastructure.

#### Network Segmentation

- Limit user access based on roles (e.g., HR staff shouldn’t access IT infrastructure).
- Ensure hosts requiring external access are properly secured and monitored.

---

## Defense-In-Depth Approach

Combining **people**, **processes**, and **technology** creates a multi-layered security posture, reducing the risk of breaches and minimizing potential damage.

By prioritizing visibility, segmentation, and proactive monitoring, organizations can effectively protect their networks while providing actionable feedback to mitigate vulnerabilities uncovered during penetration testing.