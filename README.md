# Path-Traversal-Wordlist

A comprehensive collection of path traversal (directory traversal) payloads specifically curated for security researchers and penetration testers. This repository contains specialized wordlists for bypassing common web application filters and Web Application Firewalls (WAFs).

## Wordlists

### [Linux-specific path traversal wordlist.txt](./Linux-specific%20path%20traversal%20wordlist.txt)
**Targets:** `/etc/passwd`, `/etc/shadow`, `/etc/hosts`, and local file inclusions.
- **Techniques:** URL Encoding, Double Encoding, Null Bytes (`%00`), Nested sequences (`....//`), and UTF-8 Overlong encoding (`..%c0%af`).

### [Windows-specific Path Traversal wordlist.txt](./Windows-specific%20Path%20Traversal%20wordlist.txt)
**Targets:** `boot.ini`, `win.ini`, `web.config`, and `system32/drivers/etc/hosts`.
- **Techniques:** Backslash/Forward-slash variations, UNC paths (`\\127.0.0.1\c$\`), NTFS Alternative Data Streams (`::$DATA`), and IIS Unicode bypasses (`..%c1%9c`).

## Usage Examples

### Caido / Burp Suite Community
1. Navigate to the **Automate** (Caido) or **Intruder** (Burp) tab.
2. Select your payload position.
3. Import the wordlist directly from this repository.
4. Filter results by **Status Code** or **Response Length** to identify successful hits.

### FFUF (Fast Fuzzer)
FFUF is a high-speed fuzzer. Use the `-mr` (match regexp) flag to identify successful file reads by searching for specific strings inside the files.

**For Linux Targets:**
```bash
ffuf -w Linux-specific-path-traversal-wordlist.txt -u [http://example.com/api/download?file=FUZZ](http://example.com/api/download?file=FUZZ) -mr "root:"

```

**For Windows Targets:**
```bash
ffuf -w ./Windows-specific-Path-Traversal-wordlist.txt -u [http://target.com/view?file=FUZZ](http://target.com/view?file=FUZZ) -mr "bit depth|extensions"
