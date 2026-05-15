# Cybersecurity SOC Home Lab: Reconnaissance and Incident Documentation

## Overview

This project documents the setup and use of a beginner SOC-style cybersecurity home lab built with VirtualBox. The lab uses Kali Linux, Metasploitable, Windows 7, and Ubuntu to practise hands-on defensive security skills, including reconnaissance analysis, exposed service identification, basic log review, and structured incident documentation.

The purpose of this project is to move beyond theory by creating a controlled environment where attacker activity can be simulated, observed, analysed, and documented from a junior SOC analyst perspective.

## Project Description

Built a SOC-style cybersecurity home lab using Kali Linux, Metasploitable, Windows 7, and Ubuntu to simulate reconnaissance, identify exposed services, analyse security events, and document investigations from a junior SOC analyst perspective.

## Objectives

* Build a controlled virtual cybersecurity lab environment.
* Simulate attacker reconnaissance using Kali Linux.
* Use Metasploitable as a vulnerable target machine.
* Identify exposed ports and services using Nmap.
* Analyse the security risks linked to exposed services.
* Document findings using a structured investigation format.
* Develop practical skills relevant to SOC analyst and cybersecurity placement roles.

## Lab Environment

| Machine        | Role                          | Purpose                                                            |
| -------------- | ----------------------------- | ------------------------------------------------------------------ |
| Kali Linux     | Attacker machine              | Used to perform reconnaissance and scanning activity               |
| Metasploitable | Vulnerable target             | Used as the intentionally vulnerable machine for testing           |
| Ubuntu         | Monitoring / analysis machine | Used for documentation, future SIEM setup, and analysis            |
| Windows 7      | Endpoint machine              | Used for future endpoint monitoring and Windows event log practice |

## Network Design

The lab is designed to run inside VirtualBox using an isolated virtual network. Vulnerable machines such as Metasploitable and Windows 7 should not be exposed directly to the internet.

Recommended network setup:

| Adapter                              | Purpose                                                                      |
| ------------------------------------ | ---------------------------------------------------------------------------- |
| NAT                                  | Allows selected machines to access the internet for updates or installations |
| Internal Network / Host-only Adapter | Allows lab machines to communicate safely inside an isolated network         |

Recommended internal network name:

```text
cyber-lab
```

## Lab Architecture

```text
Host Machine
│
└── VirtualBox Lab Network
    │
    ├── Kali Linux
    │   └── Role: Attacker machine
    │
    ├── Metasploitable
    │   └── Role: Vulnerable target
    │
    ├── Ubuntu
    │   └── Role: Monitoring / analysis machine
    │
    └── Windows 7
        └── Role: Windows endpoint for future monitoring
```

## Tools Used

* VirtualBox
* Kali Linux
* Metasploitable
* Windows 7
* Ubuntu
* Nmap
* Linux terminal commands
* Markdown documentation
* MITRE ATT&CK Framework

## Skills Practised

* Virtual machine setup
* Lab network configuration
* Basic attacker reconnaissance
* Network scanning
* Service enumeration
* Attack surface analysis
* Security documentation
* Incident investigation writing
* MITRE ATT&CK mapping

## First Investigation

### Investigation 01: Nmap Reconnaissance Against Metasploitable

The first investigation focuses on using Kali Linux to perform an Nmap scan against the Metasploitable target machine. The aim is to identify open ports, running services, and possible security risks linked to exposed services.

Example commands:

```bash
nmap -sV <target-ip>
nmap -A <target-ip>
```

## Planned Repository Structure

```text
cybersecurity-soc-home-lab/
│
├── README.md
├── lab-architecture.md
├── setup-notes.md
├── investigations/
│   └── 01-nmap-reconnaissance.md
├── screenshots/
│   ├── virtualbox-vms.png
│   ├── kali-ip-address.png
│   ├── metasploitable-ip-address.png
│   └── nmap-scan-results.png
└── reflection.md
```

## Expected Outcome

By completing this lab, I aim to demonstrate practical understanding of how reconnaissance activity is performed, how exposed services increase an organisation's attack surface, and how findings can be documented clearly from a defensive cybersecurity perspective.

This project will continue to grow as I add more investigations, including failed login analysis, Windows event log review, SIEM setup, and basic incident triage.

## Future Improvements

* Add Wazuh SIEM on Ubuntu.
* Connect Windows 7 as a monitored endpoint.
* Generate and investigate failed login attempts.
* Add screenshots of alerts and logs.
* Create custom detection notes.
* Map more activities to MITRE ATT&CK.
* Expand the lab into a full SOC-style detection environment.

