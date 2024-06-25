# Building a SOC + Honeynet in Azure with Live Traffic
![322930551-ca6ef315-dcbf-4176-b90f-c46a6bbf0459](https://github.com/UdoWilliams/Azure-Honeynet-Soc/assets/148285991/aa1cab61-4e55-47b5-850a-8a723880202b)

# Introduction
In this project, I constructed a small honeynet within Azure, capturing logs from diverse sources into a Log Analytics Workspace. Microsoft Sentinel leverages this data to construct attack maps, generate alerts, and initiate incident responses. I assessed security metrics in an insecure environment over a 4-hour period, implemented security measures to fortify the environment, conducted another 4-hour metric assessment, and documented the findings. The metrics to be gathered include:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

# Objective
The primary goal of this project was to configure intentionally vulnerable virtual machines within Azure infrastructure to attract and analyze cyber attacks. This initiative enhanced my understanding of attacker tactics and techniques, demonstrating my capability to promptly and effectively address identified vulnerabilities.

# Technologies, Regulations, and Azure Components Employed:

- Azure Virtual Network (VNet)
- Azure Network Security Group (NSG)
- Virtual Machines (2x Windows, 1x Linux)
- Log Analytics Workspace with Kusto Query Language (KQL) Queries
- Azure Key Vault for Secure Secrets Management
- Azure Storage Account for Data Storage
- Microsoft Sentinel for Security Information and Event Management (SIEM)
- Microsoft Defender for Cloud to Protect Cloud Resources
- Windows Remote Desktop for Remote Access
- Command Line Interface (CLI) for System Management
- PowerShell for Automation and Configuration Management
- NIST SP 800-53 Revision 5 for Security Controls
- NIST SP 800-61 Revision 2 for Incident Handling Guidance

# Methodology
- Creating the honeynet: Initially, I deployed multiple vulnerable virtual machines in Azure to simulate an insecure environment.

- Monitoring and analysis: Azure was configured to collect log data from various resources into a log analytics workspace. Using Microsoft Sentinel, I constructed attack maps, triggered alerts, and managed incidents based on the gathered information.

- Security metrics assessment: Over a 4-hour period, I monitored the environment while it remained insecure, capturing essential security metrics. This served as a benchmark for comparison post-implementation of remedial actions.

- Incident response and remediation: Following the identification of vulnerabilities and resolution of incidents, I initiated the hardening process by implementing security best practices and adhering to Azure-specific recommendations.

- Post-remediation evaluation: Subsequently, I conducted another 4-hour observation of the environment to reassess security metrics, comparing them against the initial baseline.

# Before Hardening / Security Controls Architecture

In![before hardeing](https://github.com/UdoWilliams/Azure-Honeynet-Soc/assets/148285991/88eba60c-82e6-491f-a945-3fb37b3ff44a)
 Azure, I created a resource group and deployed a Windows virtual machine and a Linux virtual machine. To simulate vulnerability, I disabled the Windows Firewall protection via Remote Desktop Protocol (RDP) for the Windows machine. Additionally, I modified the network security group (NSG) associated with the Windows machine to allow all inbound traffic by using the wildcard input `*`. Similarly, for the Linux machine, I adjusted the NSG to permit all inbound traffic using the wildcard `*`.

In the "BEFORE" stage of the project, all resources were initially deployed with public exposure to the internet. This setup was intentionally insecure to attract potential cyber attackers and observe their tactics. The Virtual Machines had both their Network Security Groups (NSGs) and built-in firewalls wide open, allowing unrestricted access from any source. Additionally, all other resources, such as storage accounts and databases, were deployed with public endpoints visible to the internet, without utilizing any Private Endpoints for added security.

# Architecture After Hardening / Security Controls

![after hardening](https://github.com/UdoWilliams/Azure-Honeynet-Soc/assets/148285991/c65a1f49-23d1-440f-9e8a-d145a0dda29e)

For hardening of our architecture I executed a comprehensive set of hardening measures and implemented robust security controls to enhance the overall security posture of the environment. These enhancements encompassed:

- **Network Security Groups (NSGs):** I tightened NSGs to permit only inbound and outbound traffic from my designated public IP address. This restriction ensured that only authorized traffic could reach the virtual machines.
  
- **Built-in Firewalls:** I configured VM-specific firewalls to restrict unauthorized access, tailoring rules to minimize potential attack vectors and safeguard resources.

- **Private Endpoints:** I replaced public endpoints with Private Endpoints for Azure resources like storage accounts and databases. This shift confined access to within the virtual network, shielding sensitive resources from external threats and unauthorized access.

  By comparing security metrics before and after implementing these hardening measures and security controls, I effectively showcased the impact of each step on enhancing the overall security posture of the Azure environment.

# Attack Maps Before Hardening / Security Controls

The attack maps utilized pre-built KQL .JSON map files extracted from a workbook. These files structured attack patterns and associated data, facilitating visualizations that vividly depicted cyber threats and their system impact.

This attack map highlights the risks of leaving the Network Security Group (NSG) open, enabling unrestricted malicious traffic. It emphasizes the need for robust security practices, such as strict NSG rules, to prevent unauthorized access and mitigate potential threats.

![malicious allowed](https://github.com/UdoWilliams/Azure-Honeynet-Soc/assets/148285991/4556bbdb-5950-4559-a7b5-2344349c4a9c)
![linux fail](https://github.com/UdoWilliams/Azure-Honeynet-Soc/assets/148285991/9150c135-b95d-4f8d-a0c6-6ccbb0870c0d)
![windows before](https://github.com/UdoWilliams/Azure-Honeynet-Soc/assets/148285991/aea3adca-c623-4b67-aaf2-f0b5d730ffbc)

# Metrics Before Hardening / Security Controls
The following table shows the metrics we measured in our insecure environment for 4 hours:
| Start Time 2024-06-24  9:00:47
| Stop Time 2024-06-24 14:00:48

Metric	Count
SecurityEvent	1988
Syslog	11
SecurityAlert	22
SecurityIncident	23
AzureNetworkAnalytics_CL	2190

  
