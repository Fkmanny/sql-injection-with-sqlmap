# Project: SQL Injection Vulnerability Assessment with SQLMap

## Overview
This project demonstrates a comprehensive SQL injection vulnerability assessment against a DVWA (Damn Vulnerable Web Application) target using SQLMap. The assessment includes database enumeration, table extraction, credential dumping, and privilege analysis to identify critical security weaknesses in web applications.

---

## Organizational Application

### Importance to Companies
This SQL injection assessment is critical for organizations to identify and remediate severe web application vulnerabilities that could lead to complete database compromise. It demonstrates the urgent need for secure coding practices, input validation, and regular security testing to protect sensitive customer and business data.

### Use Case Scenario
An e-commerce company conducts regular SQL injection testing to prevent data breaches that could expose customer payment information, ensuring PCI-DSS compliance and maintaining customer trust in their online platform.

---

## Configuration & Screenshots

### 1. Network Configuration Verification
- Verified Kali Linux network configuration using ifconfig
- Identified IP address and network interface details
- Established baseline network connectivity for targeting

![Ifconfig Command on Kali](screenshots/kali-ifconfig.png)
*Kali Linux network configuration showing IP address and interface details*

### 2. Host Discovery with Fping
- Scanned entire subnet (192.168.56.0/24) for alive hosts
- Used fping with quiet mode and statistics output
- Identified responsive hosts within the target network

![Fping Host Discovery](screenshots/fping-scan.png)
*Active host discovery using fping showing responsive systems and statistics*

### 3. NetBIOS Identification with Nbtscan
- Scanned network for NetBIOS information and host identification
- Located Metasploitable machine through service enumeration
- Gathered hostname and MAC address information

![Nbtscan Results](screenshots/nbtscan-results.png)
*NetBIOS scanning identifying Metasploitable target system with hostname details*

### 4. DVWA SQL Injection Target
- Accessed DVWA web application with default credentials
- Configured security level to low for vulnerability testing
- Navigated to SQL injection vulnerability page

![DVWA SQL Injection Page](screenshots/dvwa-sql-injection-page.png)
*DVWA SQL injection vulnerability page with low security settings*

### 5. Privilege Escalation
- Switched to root user for administrative privileges
- Prepared environment for SQLMap tool execution
- Ensured proper permissions for comprehensive testing

![Root Privilege Access](screenshots/root-privilege-access.png)
*Root user access established for SQLMap tool execution*

### 6. Database Enumeration
- Executed SQLMap to enumerate all available databases
- Used session cookies for authenticated testing
- Discovered multiple databases including sensitive systems

![Database Enumeration](screenshots/database-enumeration.png)
*SQLMap database enumeration showing all available databases on target*

![Database List Results](screenshots/database-list-results.png)
*Complete list of discovered databases including dvwa, metasploit, and mysql*

### 7. Table Extraction from DVWA Database
- Targeted DVWA database for table enumeration
- Extracted table structure and relationships
- Identified critical user data tables

![DVWA Table Extraction](screenshots/dvwa-table-extraction.png)
*Table enumeration within DVWA database showing guestbook and users tables*

### 8. User Data Extraction
- Dumped complete contents of users table
- Extracted username and password hashes
- Retrieved sensitive authentication information

![User Data Extraction](screenshots/user-data-extraction.png)
*Complete user data extraction from DVWA users table*

![User Credentials Results](screenshots/user-credentials-results.png)
*Retrieved usernames and password hashes from compromised user table*

### 9. Credential Verification
- Verified extracted credentials through successful login
- Demonstrated practical impact of SQL injection vulnerability
- Confirmed authentication bypass capability

![Credential Verification](screenshots/credential-verification.png)
*Successful login using compromised Pablo credentials*

### 10. Database Privilege Analysis
- Enumerated database user privileges and permissions
- Identified privilege escalation opportunities
- Mapped user access levels and capabilities

![Privilege Analysis Part 1](screenshots/privilege-analysis-1.png)
*Database user privilege enumeration showing root user capabilities*

![Privilege Analysis Part 2](screenshots/privilege-analysis-2.png)
*Continued privilege analysis showing user permission differences*

![Privilege Analysis Part 3](screenshots/privilege-analysis-3.png)
*Complete privilege mapping showing total privilege counts per user*

---

## Observations and Challenges

### Technical Challenges
- **Session Management**: Required proper cookie handling for authenticated SQL injection tests
- **Network Connectivity**: Initial host discovery needed precise subnet targeting
- **Tool Configuration**: SQLMap required specific parameters for different enumeration phases

### Security Findings
- **Critical Vulnerability**: SQL injection allowed complete database compromise
- **Weak Authentication**: Default credentials and low security settings enabled easy access
- **Privilege Issues**: Excessive database privileges present on multiple accounts

### Performance Considerations
- **Scan Efficiency**: SQLMap provided comprehensive enumeration with minimal requests
- **Network Impact**: Scans conducted with consideration for network performance
- **Time Optimization**: Batch mode accelerated testing process

---

## Reflections

### Technical Insights
- **SQL Injection Impact**: Demonstrated severe consequences of injection vulnerabilities
- **Database Security**: Highlighted importance of proper database hardening
- **Tool Effectiveness**: SQLMap proved extremely effective for comprehensive testing

### Security Implications
- **Authentication Weaknesses**: Default credentials create immediate security risks
- **Privilege Management**: Excessive privileges significantly increase attack surface
- **Web Application Security**: Critical need for input validation and parameterized queries

### Operational Lessons
- **Methodical Approach**: Importance of structured testing methodology
- **Documentation Value**: Comprehensive logging essential for analysis and reporting
- **Ethical Considerations**: Responsible disclosure and testing practices

---

## How to Reproduce

### Prerequisites
- Kali Linux penetration testing distribution
- Metasploitable 2 or DVWA vulnerable web application
- Network connectivity between testing and target systems
- Administrative privileges on testing machine

### Implementation Steps

1. **Network Configuration Verification**
```bash
ifconfig
ip addr show
```

2. **Host Discovery**
```bash
fping -s -a -g -q 192.168.56.0/24
nbtscan 192.168.56.0/24
```

3. **DVWA Access**
```bash
# Access DVWA in browser
http://192.168.56.103/dvwa

# Login credentials
Username: admin
Password: password

# Set security to low
```

4. **Privilege Escalation**
```bash
sudo su
```

5. **Database Enumeration**
```bash
sqlmap -u "http://192.168.56.103/dvwa/vulnerabilities/sqli/?id=234" --cookie="PHPSESSID=..." --batch --dbs
```

6. **Table Extraction**
```bash
sqlmap -u "http://192.168.56.103/dvwa/vulnerabilities/sqli/?id=1" --cookie="..." -D dvwa --batch --tables
```

7. **Data Extraction**
```bash
sqlmap -u "http://192.168.56.103/dvwa/vulnerabilities/sqli/?id=1" --cookie="..." -D dvwa -T users --batch --dump
```

8. **Privilege Analysis**
```bash
sqlmap -u "http://192.168.56.103/dvwa/vulnerabilities/sqli/?id=1" --cookie="..." --privileges --batch
```

9. **Credential Verification**
```bash
# Manual login verification with extracted credentials
Username: pablo
Password: letmein
```
