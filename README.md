![image](https://github.com/user-attachments/assets/2ff0f189-f94a-4e57-ad64-c175d58cdbe9)# Azure-SOC-Honeynet-Project (Live Traffic)

![Cloud Honeynet / SOC](https://i.imgur.com/rj5UWwN.png)

## Introduction
This tutorial will teach you how to set up and secure a honeynet on Microsoft Azure. A honeynet is a network designed to attract attackers so you can study their behaviors and improve security measures. This tutorial will guide you through the steps from creating a vulnerable honeynet environment to securing it using best practices aligned with NIST standards.

## Objectives
1. Build a Honeynet: Construct a honeynet to simulate real-world cyberattacks and analyze attacker behaviors and tactics.
2. Secure the Environment: Enhance security by reconfiguring network settings and applying security controls recommended by NIST 800-53 and Microsoft Defender for Cloud.

## Before Hardening

![Before](https://i.imgur.com/WVa7UIB.png)

## After Hardening

![After](https://i.imgur.com/YHU5fm4.png)

## Technologies, Regulations, and Azure Components Employed:

- Microsoft Azure Services:
- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 Windows, 1 Linux)
- Azure Key Vault to securely store secrets
- Azure Storage for storing data
- Microsoft Sentinel for Security Information and Event Management (SIEM).
  
- Security Tools:
- Log Analytics Workspace for Kusto Query Language (KQL) queries to filter data
- Microsoft Defender for Cloud to monitor resources and ingest logs from virtual machines into Log Analytic Workspace
- PowerShell for attack simulations.
  
- Regulatory Compliance:
- NIST SP 800-53 for security controls
- NIST SP 800-61 for incident response.


## Phase I - Creating The Honeynet 
1. Setup Virtual Machines: Deploy two Windows and one Linux virtual machine on Azure.
2. Configure Network Settings: Intentionally weaken the firewall settings and Network Security Groups to allow all incoming and outgoing traffic, making the VMs susceptible to attacks.


![Firewallrule](https://i.imgur.com/QNfVI72.jpg)

## Phase II - Simulated Attacks and Monitoring
1. Execute Simulated Attacks: Use PowerShell scripts to simulate various cyberattacks like brute force attempts and privilege escalation.
2. Log and Monitor Activities: Utilize Azure's Log Analytics Workspace to run KQL queries that filter and analyze the data from these simulated attacks, capturing real-time events and alerts.


SecuityEvent logs display brute force attacks against Windows virtual machines 

![SecurityEvent](https://i.imgur.com/saEAPDm.png)

![SecurityEvent](https://i.imgur.com/y8sQDD1.jpg)

Syslog display failed password against Linux virtual machine

![Syslog](https://i.imgur.com/41XpjMJ.png)

![Syslog](https://i.imgur.com/KP4NoPt.png)

SecurityAlert (Microsoft Defender for Cloud)

![SecurityAlert](https://i.imgur.com/ljaMPsJ.png)

![SecurityAlert](https://i.imgur.com/fD4fh0o.png)

SecurityIncident (Sentinel Incidents)

![SecurityIncident](https://i.imgur.com/Ff1a9qT.png)

![SecurityIncident](https://i.imgur.com/ZsNHqMg.png)

NSG Inbound Malicious Flows Allowed

![NSG Inbound Malicious](https://i.imgur.com/YRy1kMm.png)

![NSG Inbound Malicious](https://i.imgur.com/5O9z1PP.png)



## Phase III - Incident Response and Analysis
1. Assess Incidents: After gathering data for 24 hours, assess each incident by investigating the source, tactics, techniques, and timeline of the attacks.
2. Classify Incidents: Determine the severity and authenticity of each incident (true positive vs. false positive).


![Incident detail](https://i.imgur.com/MEIisRs.jpg)

![Incident Visual Investigation](https://i.imgur.com/m8J3GEt.jpg)

## Phase IV - Remediation and Regulatory Compliance 

  1. Enhance VM's security by implement controls that follow the NIST 800-53 and SP 800-61 regulatory compliance standards:
   - Disabling public access to the virtual machines and blob storage account.
   - Creating private endpoints for the storage account and virtual machine.
   - Setting up additional Network Security Groups to protect subnets.
   - A NSG rule was generated for these virtual machines to only allow traffic from my own IP source address.
   - private links were enabled to keep key vault safe.
 
- A Network Security Group (NSG) implements security rules regulating inbound and outbound network traffic by specifying allowed or denied protocols, source and destination IP addresses, and port numbers.
- A private endpoint is a network interface that enhances security by restricting resource access to the private network domain, shielding it from exposure to the public internet.
- NIST SP 800-53 provides a framework of security controls aimed at assisting organizations in defending against security threats and vulnerabilities.
- NIST SP 800-61  is designed to provide organizations with a framework for establishing an incident response program.

## Phase V - Results and Reflection
1. Analyze Before and After Metrics: Compare the number of attacks and types of traffic before and after the security enhancements to evaluate the effectiveness of your security measures.
2. Reflect on Learning: Understand the critical role of correct security configurations and controls in protecting network resources.
  

## Before Hardening 

This attack world map accentuates how many attacks the Windows virtual machine encountered

![Windows World Map](https://i.imgur.com/o9EMfkH.png)


This attack world map depicts the number of attacks targetted to the Linux virtual machine

![Syslog World Map](https://i.imgur.com/DgsdQ63.png)


This attack world map represents the large influx of malicious traffic resulted from insecure environment 

![NSG World Map](https://i.imgur.com/qXM3PJ5.png)

Metrics were collected from 2023-05-08 at 18:50 - 2023-05-09 at 18:50.

![Before Metrics](https://i.imgur.com/9E65SUn.png)

## After Hardening

Attack world maps displayed no results, indicating that there has not been any new attacks after securing the environment.  

Metrics were collected from 2024-08-14 at 18:19 to 2024-08-15 at 18:19.

![Before Metrics](https://i.imgur.com/ug7mWjY.png)


## Conclusion
Following this tutorial, you will create a functional honeynet on Azure and gain valuable insights into cybersecurity threats and defense mechanisms. This exercise highlights the importance of proactive security practices in maintaining and securing IT environments against evolving cyber threats.
