  ## *PASSWORD CRACKING* ##
# PDF Password Cracking Lab | John the Ripper & NetworkWalks

![Kali Linux](https://img.shields.io/badge/Platform-Kali%20Linux-blue?logo=kalilinux)
![John the Ripper](https://img.shields.io/badge/Tool-John%20the%20Ripper-red)
![Cybersecurity](https://img.shields.io/badge/Domain-Password%20Security-orange)
![Status](https://img.shields.io/badge/Status-Completed-success)

## Overview

This repository documents my hands-on password-cracking exercise involving password-protected PDF files using **John the Ripper** and the online password-cracking tool provided by **NetworkWalks**.

The objective of this exercise was to understand how password-protected PDF files can be audited, how password hashes can be extracted and processed, and how dictionary-based password attacks with rule-based wordlist mutations work.

All PDF files used in this exercise were provided as part of an authorized cybersecurity training assignment.

## Tools & Technologies

| Tool | Purpose |
|---|---|
| Kali Linux | Penetration testing environment |
| John the Ripper | Offline password hash cracking |
| NetworkWalks Online Tool | Online PDF password-cracking exercise |
| PDF Hash Extraction | Preparing PDF password hashes |
| Wordlists | Dictionary-based password testing |

## Lab Resources

The provided lab files and supporting materials are available here:

**[Google Drive – Password Cracking Lab Files](https://drive.google.com/drive/folders/1BipNY5NSQpPB3KSJwdJiu6X0VA1FVbcM)**

## Part 1: Password Cracking with John the Ripper

I used John the Ripper to recover passwords from three password-protected PDF files.

### Methodology

1. Obtained the provided password-protected PDF files.
2. Extracted their password hashes into separate text files.
3. Used John the Ripper with the supplied password wordlist.
4. Enabled password mutation rules using `--rules`.
5. Successfully recovered all three PDF passwords.

### Command Used

```bash
john --wordlist=/usr/share/john/password.lst --rules hash1.txt
```

The same command was used for the remaining hash files:

```bash
john --wordlist=/usr/share/john/password.lst --rules hash2.txt

john --wordlist=/usr/share/john/password.lst --rules hash3.txt
```

### Results

All three PDF passwords were successfully recovered.

| PDF File | Recovered Password | Result |
|---|---|---|
| my locked pdf1.pdf | `good-luck` | Successfully cracked |
| my locked pdf2.pdf | `password1` | Successfully cracked |
| my locked pdf3.pdf | `1qaz2wsx` | Successfully cracked |

### Terminal Output Highlights

**Hash 1:**
```text
Loaded 1 password hash
Cost 1 (revision) is 4
Will run 12 OpenMP threads

good-luck        (?)
1g ... DONE
Session completed.
```

**Hash 2:**
```text
Loaded 1 password hash
Will run 12 OpenMP threads

password1        (?)
1g ... DONE
Session completed.
```

**Hash 3:**
```text
Loaded 1 password hash
Will run 12 OpenMP threads

1qaz2wsx         (?)
1g ... DONE
Session completed.
```

## Part 2: Password Cracking with NetworkWalks

For the second part, I used the online password-cracking tool provided by NetworkWalks.

### Target File

`my locked pdf1(for nw tools lab wk3-pm2).pdf`

### Procedure

1. Opened the NetworkWalks password-cracking tool.
2. Uploaded the provided password-protected PDF.
3. Initiated the password-cracking process.
4. Retrieved the resulting password and completed the associated lab objective.
5. Captured the flag provided by the exercise.

### Result

The NetworkWalks exercise was successfully completed, and the associated flag was captured.

## Part 3: Captured Flags

The following flags were obtained during the exercises.

| Flag | Captured Value |
|---|---|
| Flag 1 | `mw{cybersecurity_flag_captured_2608}` |
| Flag 2 | `nw{networkwalks_persistence_jtr_270521}` |
| Flag 3 | `nw{networkwalks_flag_260821_1}` |
| NetworkWalks PDF Flag 1 | `nw{networkwalks_flag1_jtr_270521_1}` |

## Key Learnings

Through this practical exercise, I gained experience with:

- Understanding password-protected PDF files.
- Extracting PDF password hashes for offline auditing.
- Using John the Ripper for dictionary-based password cracking.
- Understanding the purpose of wordlists and password mutation rules.
- Running password-cracking sessions with multiple CPU threads.
- Interpreting John the Ripper terminal output.
- Understanding the role of online password-auditing tools.
- Recognizing the importance of strong and unpredictable passwords.

## Security Takeaways

This exercise demonstrated why relying on common passwords is risky.

Passwords such as `password1`, `good-luck`, and predictable keyboard patterns can potentially be recovered through dictionary-based attacks when the corresponding password hashes are available.

**Recommended security practices:**

- Use long and unique passwords.
- Avoid dictionary words and predictable keyboard patterns.
- Use a password manager to generate and store strong passwords.
- Apply appropriate encryption to sensitive PDF documents.
- Never reuse passwords across different services.

## Final Status

**Lab Status: Successfully Completed**

| Activity | Status |
|---|---|
| John the Ripper – PDF 1 | Completed |
| John the Ripper – PDF 2 | Completed |
| John the Ripper – PDF 3 | Completed |
| NetworkWalks – PDF Exercise | Completed |
| Flag Collection | Completed |

## Disclaimer

This project is intended strictly for educational purposes and authorized cybersecurity training.

All password-cracking activities were performed on files provided for the assigned lab exercise. Do not attempt to crack passwords or access files without explicit authorization.

---

**Author:** Dinesh  
**Environment:** Kali Linux  
**Focus:** Ethical Hacking | Penetration Testing | Password Security

