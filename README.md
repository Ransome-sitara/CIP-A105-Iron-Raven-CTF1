# OPERATION IRON RAVEN
## CIP-A105 - Offensive Security Operations II
### CTF 1 Summative Competency Exam

---

## Student Information

| Field | Value |
|-------|-------|
| Name | Daniel Etim |
| Registration Number | 2026/EHIT/16917 |
| Course | Offensive Security Operations II (CIP-A105) |
| Assessment | CTF 1 - Summative Competency Exam |
| Operation | OPERATION IRON RAVEN |
| Target | OPFOR-01 (Raven) |
| Submission Date | 16 September 2026 |

---

## Overview

This repository contains the complete submission package for the CIP-A105 CTF 1 competency exam. The assessment was a black-box penetration test against OPFOR-01, a standalone Linux server designated as Raven, conducted inside an isolated laboratory network.

---

## Summary of Findings

| Category | Count |
|----------|-------|
| Critical findings | 2 |
| High findings | 1 |
| Medium findings | 6 |
| Low findings | 3 |
| Mission artifacts recovered | 1 |
| Initial access achieved | No |

### Key Findings

| ID | Finding | Severity |
|----|---------|----------|
| F-01 | WordPress 4.8.7 with 71 known CVEs | Critical |
| F-02 | PHPMailer 5.2.16 CVE-2016-10033 | Critical |
| F-03 | Exposed vendor directory | High |
| F-04 to F-09 | User enumeration, XML-RPC, source disclosure, directory listing, cookie flags, no lockout | Medium |
| F-10 to F-12 | Apache manual, .DS_Store, IP leak | Low |

### Recovered Artifacts

| Artifact | Path | SHA-256 |
|----------|------|---------|
| flag3.png | /wordpress/wp-content/uploads/2018/11/ | 2479b9ab0c0763bf9bdc4c2fc36c701001a013a557a5a9f6beda44b024d9cc2e |
| contact.zip | /contact.zip | a265aefd879bd7db6473a4ba79f7628d370a61208f8dc011f506fe826854c433 |

---

## Repository Structure

CIP-A105-Iron-Raven-CTF1/
├── OPERATION-IRON-RAVEN-Report.pdf # Full penetration test report
├── operator-log.txt # Chronological activity log
├── evidence/
│ ├── screenshots/ # 24 evidence screenshots
│ ├── scans/ # 7 scan outputs (Nmap, Gobuster, RPC)
│ ├── hashes/ # SHA-256 hashes for baseline and artifacts
│ ├── logs/ # Phase preparation and recon logs
│ └── artifacts/ # Recovered mission artifacts
└── README.md


---

## Methodology

### Phase 0: Preparation
- Preserved original VMDK and created clean baseline
- Verified network isolation
- Created evidence directory and operator log

### Phase 1: Reconnaissance
- ARP scan and ICMP ping sweep on 10.10.10.0/24
- Discovered target at 10.10.10.157
- Confirmed TTL 64 (Linux OS)

### Phase 2: Attack-Surface Enumeration
- Full TCP port scan (all 65535 ports)
- UDP scan (top 50 ports)
- Service version detection
- Directory brute force with Gobuster
- WordPress enumeration with WPScan
- PHPMailer vendor directory analysis

### Phase 3: Vulnerability Analysis
- Version-to-CVE mapping
- Source code review (contact.php)
- Injection testing (SQL, command, template)
- Authentication and session analysis

### Phase 4: Initial Access
- PHPMailer sendmail injection testing
- File upload testing
- XML-RPC and REST API testing
- Comment posting and trackback testing

---

## Tools Used

| Tool | Purpose |
|------|---------|
| QEMU | Target virtualization |
| dnsmasq | DHCP for isolated network |
| Nmap | Port scanning and service detection |
| Gobuster | Directory enumeration |
| WPScan | WordPress enumeration |
| curl | Manual HTTP testing |
| Burp Suite | Request interception |
| Firefox | Manual web interaction |

---

## Environment Restoration

The target environment was restored to its clean baseline after the assessment.

| Item | Status |
|------|--------|
| Test artifacts written | None |
| Test comments posted | None |
| QEMU state | Stopped |
| Baseline hash | 06b6b9f0acec6d6f923ed2207ef925af1807d66fcd26cd1c7e4a6e59059660ac |
| Restored image hash | 06b6b9f0acec6d6f923ed2207ef925af1807d66fcd26cd1c7e4a6e59059660ac |
| Hash match | Confirmed |

---

## Remediation Summary

### Immediate (0-7 days)
- Upgrade WordPress to latest stable version
- Upgrade PHPMailer to 6.0 or later
- Block access to /vendor/
- Remove contact.zip from web root
- Disable directory listing

### Short-Term (1-4 weeks)
- Add HttpOnly, Secure, SameSite cookie flags
- Implement rate limiting on login
- Remove /manual/
- Block dotfiles
- Sanitise RSS feed GUIDs

### Strategic (1-3 months)
- Web Application Firewall
- Vulnerability management programme
- Regular penetration testing
- SIEM deployment

---

## Conclusion

The assessment identified a target with multiple security weaknesses but no reachable exploitation path from an unauthenticated position. The PHPMailer vulnerability requires a working MTA that is not present. WordPress 4.8.7 CVEs require authentication that was not obtained.

The single mission artifact flag3.png was located through methodical directory enumeration.

---

## Disclaimer

This assessment was conducted in a controlled laboratory environment as part of the CIP-A105 course at ICDFA. All activity was confined to the authorised OPFOR-01 target. No production systems were touched.

**Classification:** TRAINING USE ONLY.
