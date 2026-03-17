# Web Application SQL Injection Assessment

![Cybersecurity](https://img.shields.io/badge/Field-Cybersecurity-blue)
![Focus](https://img.shields.io/badge/Topic-Web%20Application%20Security-orange)
![Technique](https://img.shields.io/badge/Vulnerability-SQL%20Injection-red)

---

## Overview

This project demonstrates a security assessment of a vulnerable web application used to retrieve student grades. The analysis focuses on identifying and exploiting SQL injection vulnerabilities that affect authentication, data confidentiality, and system integrity.

Through manual testing, the application was shown to allow unsanitised user input to be inserted directly into database queries. This weakness enabled an attacker to enumerate database structures, extract sensitive information, bypass authentication controls, and manipulate stored data.

The exercise illustrates how improperly validated input and insecure database design can lead to full compromise of a web application.

---

## Key Vulnerabilities Identified

Several critical vulnerabilities were discovered during the assessment:

* SQL Injection in user input fields
* Authentication bypass through injected SQL conditions
* Database schema enumeration
* Plaintext password storage
* Unrestricted access to sensitive records
* Data integrity manipulation through backend logic

These vulnerabilities collectively affect all three major security properties: confidentiality, integrity, and authentication.

---

## Attack Workflow

The exploitation process followed several stages.

### 1. SQL Injection Discovery

Testing the COMP code input field revealed that user input was directly inserted into the SQL query. Injecting a tautology (`' OR '1'='1`) caused the application to return multiple rows, confirming the presence of SQL injection.

### 2. Authentication Bypass

The login form was vulnerable to SQL injection in the password field. By injecting a tautology, the authentication query always evaluated to true, allowing access to the system without valid credentials.

### 3. Viewing All Grades

Manipulating module queries with injected conditions allowed the application to return grades for multiple users rather than the authenticated user.

### 4. Database Enumeration

Using UNION-based SQL injection techniques, the structure of the database was enumerated. The attacker identified key schemas and tables including:

* `users`
* `grades`
* `sessions`

Additional queries were used to retrieve column names from these tables.

### 5. Credential Extraction

Further SQL injection queries allowed the extraction of all usernames and passwords stored in the database.

Filtering results for non-student accounts revealed privileged credentials such as:

* admin
* school

The system stored passwords in plaintext, allowing immediate credential compromise.

### 6. Integrity Manipulation

The application allowed manipulation of the displayed grade value using UNION queries. When the "Try Harder" button was triggered, the backend incremented the manipulated value and permanently wrote it to the database.

This demonstrated how SQL injection could be used not only to read data but also to alter stored records.

---

## Security Impact

The identified vulnerabilities enable several severe attack scenarios:

* Full database disclosure
* Credential theft and privilege escalation
* Authentication bypass
* Permanent modification of stored academic records

These weaknesses demonstrate the risks of unsanitised input, improper database design, and missing access control mechanisms.

---

## Tools Used

* Kali Linux
* Manual SQL injection techniques
* Browser-based testing
* Database enumeration queries

---

## Repository Structure

```
webapp-sql-injection-lab/
│
└── docs/
    └── web-application-security-laboratory.pdf
├── .gitignore
├── LICENSE
├── README.md

```

---

## Security Note

The techniques demonstrated in this project are intended for security testing, vulnerability research, and defensive training. Understanding how SQL injection works is essential for building secure web applications and preventing data breaches.

---

## Author

Arka Paul
Cyber Security

