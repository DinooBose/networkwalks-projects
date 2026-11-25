
Mediroza General Hospital --- VAPT Assessment

Report ID: MED-VAPT-2026-01
Assessment period: 24--25 November 2026
Assessment type: Black-box, time-boxed CTF assessment
Environment: Mediroza CTF training environment
Classification: Confidential --- Training / CTF Assessment
Overview

This repository contains documentation and supporting evidence for a
black-box vulnerability assessment and penetration-testing exercise
against the Mediroza CTF environment.

The assessment focused on public-facing web application behavior,
authentication-page observations, exposed resources, network service
enumeration, and password recovery of explicitly designated CTF PDF
challenge files.

This README distinguishes directly observed behavior from unverified or
challenge-supplied information. It does not claim successful
patient-portal authentication, successful SQL injection exploitation, or
independent verification of the live SQL backup contents.
Assessment Scope

Item Details

Target domain medirozahospital.com

Resolved IPv4 address 199.188.201.16

Application paths observed /, /patient/login.php,
/staff/login.php,
/old/mediroza_db_backup_2019.sql

Assessment approach Black-box / time-boxed CTF exercise

Tools evidenced Nmap, curl, THC Hydra, John the
Ripper
Assessment dates 24--25 November 2026

Testing was limited to the stated CTF scope and retained evidence. No
patient records were accessed, no database contents were extracted, and
no candidate credentials were used to sign in.
Executive Summary

The assessment produced these observations:

    A single quote in the patient-login username field caused a MySQLi
    SQL syntax warning to be displayed.
    A request for the SQL backup resource returned HTTP 200 OK. The
    live backup contents were not independently retrieved or verified
    for this report. The SQL excerpt supplied as CTF challenge material
    describes staff and shareholder tables.
    Password recovery was reported successful for three designated CTF
    PDF challenge files. Password values are intentionally omitted.
    A Hydra run reported a candidate credential, but its configured
    failure marker differed in capitalization from the application's
    observed failure message. The result is inconclusive and may be a
    false positive.
    Nmap service/version enumeration reported multiple externally
    reachable TCP services.

Findings Register

ID Finding Assessment status

MED-001 SQL syntax error Observed; SQL injection
disclosed by patient exploitability
login unconfirmed

MED-002 SQL database backup HTTP accessibility
resource publicly observed; live contents
reachable unverified

MED-003 Weak passwords on Recovery reported
designated CTF PDF successful for 3 of 3
documents CTF files

MED-004 Hydra patient-login Inconclusive; not a
result confirmed vulnerability
MED-005 Multiple network Service enumeration
services exposed observed; exposure
review recommended
MED-001 --- SQL Error Disclosure

The patient login page displayed a mysqli_query() SQL syntax warning
after a single quotation mark was submitted in the username field.

What this establishes: database error details are exposed to the
client, and input handling warrants review.

What this does not establish: successful SQL query manipulation,
authentication bypass, database extraction, or access to patient
records.

Recommendation: use parameterized/prepared SQL statements, bind all
user-controlled values, disable detailed error display in production,
and log database exceptions server-side.
MED-002 --- Publicly Reachable SQL Backup

The earlier HTTP metadata capture for /old/mediroza_db_backup_2019.sql
showed:

    HTTP status: 200
    Content type: text/x-sql
    Content length: 6346 bytes

The supplied CTF SQL excerpt describes staff and shareholders
tables, including personal, compensation, and ownership-related fields.
The live backup contents and their authenticity were not independently
verified in this report.

Recommendation: remove backup files from public web directories,
store backups outside the web root, restrict access, and review access
logs.
MED-003 --- CTF PDF Password Recovery

Password recovery was reported successful for all three designated CTF
PDF challenge files. Recovered passwords are deliberately omitted from
this README and the main report.

Recommendation: use long, unique, randomly generated passwords for
sensitive documents and enforce access controls at the storage layer.
MED-004 --- Hydra Result (Inconclusive)

Hydra reported a candidate credential after five attempts. The
configured failure marker was Incorrect password, while the observed
application message was Incorrect Password. The capitalization
mismatch may have caused a failed login to be interpreted as a success.

Conclusion: this is not evidence of a valid credential or a
confirmed authentication vulnerability. Do not use the reported
candidate to access the portal.
MED-005 --- Network Service Enumeration

The supplied Nmap output identified 12 open TCP ports in the default
1,000-port scan:

21, 25, 26, 53, 80, 110, 143, 443, 465, 587, 993, 995

Reported services included FTP, SMTP, DNS, HTTP proxy, POP3, IMAP, and
TLS-associated variants.

Recommendation: confirm the business need for each exposed service,
disable unused services, restrict access where possible, and review
patching and service hardening.
Methodology

The documented assessment activities included:

    Public DNS and domain-registration reconnaissance.
    Review of public pages and selected HTTP response metadata.
    Review of authentication-page behavior.
    Low-impact HTTP metadata checks for selected public paths.
    Nmap service/version enumeration.
    Documentation of the patient-login SQL error response.
    Password-recovery results for designated synthetic CTF PDF files.
    Evidence capture and documentation.

Evidence Directory Guide

The following is the recommended evidence structure for this assessment:
Mediroza-Pentest/
├── evidence/
│   ├── auth/
│   │   └── MED-AUTH-001-hydra-result.txt
│   ├── pdf-recovery/
│   │   └── MED-DATA-001-weak-pdf-passwords.txt
│   ├── public-paths/
│   │   └── MED-003-public-database-backup.txt
│   ├── sqli/
│   │   └── MED-SQLI-001-patient-login.txt
│   └── ...
├── findings/
└── reports/
    ├── Mediroza_VAPT_Report_M4.pdf
    └── Mediroza_VAPT_Report_M4.docx

This directory tree is a documentation guide. Confirm actual files and
paths in your local workspace before submitting or publishing the
repository.
Remediation Priorities

    Remove the publicly reachable SQL backup from the web root and
    investigate exposure.
    Correct patient-login SQL query handling with prepared statements.
    Disable detailed database errors in production responses.
    Review the necessity and security configuration of exposed network
    services.
    Review authentication monitoring and rate limiting using only
    instructor-approved synthetic accounts.
    Apply strong, unique document passwords and appropriate storage
    access controls.
    Review browser-security headers and deploy suitable policies after
    compatibility testing.

Limitations

    This README is based on retained assessment notes and supplied
    screenshots.
    The supplied SQL excerpt is treated as CTF challenge material; its
    authenticity and relationship to real production records are not
    established.
    The SQL backup's HTTP reachability was observed, but its live
    contents were not independently verified for this report.
    The Hydra result is inconclusive because of the failure-marker
    mismatch.
    The SQL error demonstrates error disclosure, not a proven
    authentication bypass or successful data extraction.
    The Nmap screenshot documents a default 1,000-port TCP scan, not a
    complete TCP/UDP inventory.
    No destructive testing, denial-of-service testing, persistence,
    privilege escalation, or access to real patient information was
    performed.

Reports

The accompanying report files are:

    Mediroza_VAPT_Report_M4.pdf
    Mediroza_VAPT_Report_M4.docx

Responsible Use

This material is intended for the authorized CTF/training exercise and
academic evaluation. Do not use observations, tools, or unverified
candidate credentials against systems or accounts outside the explicitly
authorized scope. Do not publish personal data, recovered passwords,
session identifiers, or confidential records.
