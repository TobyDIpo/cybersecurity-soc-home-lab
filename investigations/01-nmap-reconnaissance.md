# Investigation: Nmap Reconnaissance
## Target Machine IP Address

The Metasploitable target machine was assigned the following IP address:

```text
192.168.0.3
```
## Attacker Machine IP Address

The Kali Linux attacker machine was assigned the following IP address:

```text
192.168.0.4
```
## Connectivity Test

A ping test was performed from the Kali Linux machine to confirm that the Metasploitable target was reachable.

```bash
ping 192.168.0.3
```
## Step 3: Run your first Nmap scan

In Kali, run:

```bash
nmap -sV 192.168.0.3
```
The scan confirmed that the target host was online and identified multiple open TCP ports. Nmap reported that 23 ports were open and 977 TCP ports were closed.

## Key Findings
| Port | Service     | Version / Notes                     | Security Concern                                                                                                                      |
| ---- | ----------- | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| 21   | FTP         | vsftpd 2.3.4                        | File transfer service exposed. This version is known to be vulnerable and could be investigated further by an attacker.               |
| 22   | SSH         | OpenSSH 4.7p1                       | Remote administration service exposed. If weak credentials are used, this could allow unauthorised access.                            |
| 23   | Telnet      | Linux telnetd                       | Insecure remote login service. Telnet does not encrypt traffic, which means usernames and passwords could be captured on the network. |
| 25   | SMTP        | Postfix smtpd                       | Mail service exposed. Could be tested for misconfiguration or abuse.                                                                  |
| 53   | DNS         | ISC BIND 9.4.2                      | DNS service exposed. Attackers may attempt version-based vulnerability checks or DNS-related enumeration.                             |
| 80   | HTTP        | Apache httpd 2.2.8                  | Web server exposed. This increases the attack surface and may allow web application testing.                                          |
| 139  | NetBIOS-SSN | Samba smbd 3.X - 4.X                | File-sharing related service exposed. Could be used for SMB enumeration.                                                              |
| 445  | NetBIOS-SSN | Samba smbd 3.X - 4.X                | SMB-related service exposed. Attackers may attempt share enumeration or known Samba vulnerabilities.                                  |
| 512  | rexec       | netkit-rsh rexecd                   | Legacy remote execution service exposed. This can be risky if misconfigured.                                                          |
| 513  | rlogin      | OpenBSD or Solaris rlogind          | Legacy remote login service exposed. This is generally insecure compared with modern remote access methods.                           |
| 1524 | bindshell   | Metasploitable root shell           | Very high-risk service because it indicates a bind shell is available on the target.                                                  |
| 3306 | MySQL       | MySQL 5.0.51a                       | Database service exposed. Could contain sensitive data or allow access through weak/default credentials.                              |
| 5432 | PostgreSQL  | PostgreSQL DB 8.3.0 - 8.3.7         | Database service exposed. May be vulnerable if poorly configured or using weak credentials.                                           |
| 5900 | VNC         | VNC protocol 3.3                    | Remote desktop service exposed. Could allow graphical access if authentication is weak.                                               |
| 6667 | IRC         | UnrealIRCd                          | IRC service exposed. This service/version is known for historic vulnerabilities.                                                      |
| 8180 | HTTP        | Apache Tomcat/Coyote JSP engine 1.1 | Web application server exposed. Could be tested for weak credentials or misconfiguration.                                             |

## Analysis

The scan shows that the Metasploitable machine has a large attack surface because many services are exposed. Services such as FTP, Telnet, SMB, MySQL, PostgreSQL, VNC, and Apache Tomcat could give an attacker multiple paths to investigate further.

The most concerning service from a defensive perspective is Telnet on port 23 because it does not encrypt traffic. This means usernames and passwords could potentially be captured if they are sent across the network.

The presence of database services such as MySQL and PostgreSQL also increases risk because exposed databases may contain sensitive information or weak/default credentials.

## Evidence

Screenshot captured:

screenshots/nmap-service-scan.png


## MITRE ATT&CK Mapping

| Tactic | Technique | Explanation |
|---|---|---|
| Reconnaissance | Active Scanning | Nmap was used to actively scan the target and identify open ports |
| Discovery | Network Service Discovery | The scan identified running services and versions on the target machine |

## Lessons Learned
This scan helped me understand how attackers identify exposed services during the reconnaissance stage. I learned that a single vulnerable machine can expose many possible entry points, especially when insecure or outdated services are enabled.

From a defensive perspective, this lab showed the importance of reducing the attack surface, disabling unnecessary services, avoiding insecure protocols such as Telnet, and monitoring for scanning activity.
