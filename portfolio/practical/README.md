# Practical

Labs, exercises, and CTF write-ups from coursework and self-study.

---

## Malware Analysis

### WinLab01 — Windows Malware Analysis

- **Environment:** FlareVM
- **Tools:** Regshot, FakeNet-NG, ProcMon

Dynamic analysis of a malware sample. Took baseline snapshots, intercepted network traffic, monitored process behavior, and documented IOCs.

---

## Penetration Testing

### CHallenger — Multi-Stage CTF

- **Techniques:** WordPress SQL injection → social engineering via email → reverse shell to internal Windows workstation

### OWASP Juice Shop

- **Tools:** Burp Suite, browser dev tools

Web application security testing against an intentionally vulnerable application.

### Pickle Deserialization RCE

Python pickle deserialization leading to remote code execution.

### SSRF/XXE Chain — CVE-2021-43798

Server-Side Request Forgery combined with XML External Entity injection.

---

## Reverse Engineering

### Lab04 — XOR Password Cracking (ELF Binary)

- **Tools:** IDA Free

Reverse engineered an ELF binary's XOR-based password validation to recover the password.

---

## Shellcode

### TTC6520-3005 — Null-Byte-Free Shellcode

- **Architecture:** x86 (32-bit)

Developed shellcode without null bytes using XOR zeroing, small registers, and arithmetic operations.

---

## Cryptography

### CTF — XOR Flag Challenge

XOR string manipulation to recover a hidden flag.

### RSA — Key Generation and Encryption

- **Tools:** Python, GeoGebra

Exercises in prime selection, key generation, modular exponentiation, and Euler's totient.

### LFSR Analysis

Analyzed Linear Feedback Shift Register sequences and their cryptographic weaknesses.

---

## Network Security

### Lab Network Audit — 192.168.1.0/24

Full security audit of a lab network. Produced both a technical report and an executive summary.

---

## Blue Team

### Virtual Company Environments

Built two complete company environments from scratch in virtual infrastructure: firewalls, backbone network, SIEM, and Domain Controller.

---

## Red Team

### Penetration Testing with YAMK

Collaborative exercise with Master's degree students — penetration testing company services.
