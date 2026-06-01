# Digital Forensics Lab — SQue Worldwide Realty Endpoint Investigation

**Examiner:** Christopher Ham  
**Program:** UofL Digital Transformation Center — Cybersecurity Workforce Program  
**Date:** June 1, 2026  
**Tool:** Autopsy 4.22.1 (Sleuth Kit)  
**Evidence:** 2020JimmyWilson.E01  
**Environment:** ProxMox / Windows 11 VM  
**Framework:** NIST SP 800-86  

---

## Case Summary

Jimmy Wilson and Billy Bob are lower-level realtors employed at SQue Worldwide Realty, Inc. who share a corporate workstation. During routine IT maintenance, personnel discovered disturbing items on the device and referred it to the digital forensics examiner. This lab documents the complete forensic examination from evidence intake through HR-ready reporting.

---

## Key Findings

| Category | Count | Notes |
|---|---|---|
| Web History | 136 | Recovered from Firefox and Edge artifacts |
| Search Queries (flagged) | 17 | Handguns, identity theft, fast getaway cars, how to disappear without a trace |
| Email Messages | 27 | 2 tagged — personal Gmail used on corporate device |
| Extension Mismatches | 6 | Files with extension not matching actual file type |
| Encryption Suspected | 4 | Flagged by Autopsy encryption detection module |
| User Content Suspected | 7 | User-created or downloaded content |
| Tagged Files | 5 | Including desktop files named "Jose Badguy" and "Robert Ripoff" |
| USB Devices Attached | 9 | External storage use recorded |

---

## Flagged Search Queries

All searches attributed to user Jimmy Wilson via `places.sqlite` (Firefox) and `WebCacheV01.dat` (Microsoft Edge).

| Search Term | Domain | Date / Time (EST) | Browser |
|---|---|---|---|
| handguns | bing.com | 2014-02-11 08:36 | Firefox |
| handguns | bing.com | 2014-02-11 08:36 | Firefox |
| handguns | bing.com | 2014-02-11 08:37 | Firefox |
| how to steal identities | bing.com | 2014-02-11 08:38 | Firefox |
| identity theft jail time | bing.com | 2014-02-11 08:42 | Firefox |
| ID Theft | yahoo.com | 2014-02-10 15:07 | Edge |
| fast getaway cars | bing.com | 2014-02-10 15:12 | Edge |
| ID Theft | yahoo.com | 2014-02-10 15:18 | Edge |
| fast getaway cars | bing.com | 2014-02-10 15:12 | Edge |
| how to disappear without a trace | bing.com | 2014-02-10 15:18 | Edge |
| how to disappear without a trace | bing.com | 2014-02-10 15:18 | Edge |

> Searches for handguns, identity theft methods, fast getaway cars, and how to disappear without a trace were conducted across two browsers on two consecutive dates, reflecting deliberate and sustained research activity.

---

## Email Evidence

| To | From | Subject | Date / Time (EST) |
|---|---|---|---|
| robert.ripoff@gmx.com | wilsonjimmy807@gmail.com | Re: New email address | 2014-02-16 14:32:15 |
| robert.ripoff@gmx.com | wilsonjimmy807@gmail.com | Re: New email address | 2014-02-16 14:32:15 |

Source: `/USERS/Jimmy Wilson/AppData/Local/Microsoft/Windows Live Mail/Gmail (wils 48a/[Gmail]/All Mail`  
Source files: `6D3E57A9-00000001.eml` and `3D6C2CD6-00000008.eml`

> The email recipient name "robert.ripoff" directly matches a desktop file found on the subject's workstation.

---

## Tagged Files

| File | Path | Significance |
|---|---|---|
| AgRobust.db | `/vol_vol6/Windows/Prefetch/` | Recently executed |
| R40599.pdf | `/vol_vol6/USERS/Jimmy Wilson/Documents/` | Document requiring content review |
| Gmail All Mail store | `/USERS/Jimmy Wilson/AppData/Local/.../[Gmail]/` | Personal Gmail on corporate device |
| Jose Badguy | `/vol_vol6/USERS/Jimmy Wilson/Desktop/` | File named for a specific individual |
| Robert Ripoff | `/vol_vol6/USERS/Jimmy Wilson/Desktop/` | Matches email contact robert.ripoff@gmx.com |

---

## Examination Procedure

**Step 1 — Environment Setup**  
Logged into ProxMox virtual infrastructure at the UofL DTC lab, booted the Windows 11 VM, and confirmed VM integrity.

**Step 2 — Evidence Intake**  
Located `2020JimmyWilson.E01` at `C:\Users\UofL Student\Documents\Forensics\`. Documented file name, full path, and file size prior to ingest. Timezone confirmed as America/New_York (EST).

**Step 3 — Case Creation and Ingest**  
Created new Autopsy case (JimmyWilson, examiner: Christopher Ham). Added `2020JimmyWilson.E01` as primary data source with all ingest modules enabled: Recent Activity, Hash Lookup, File Type Identification, Extension Mismatch Detector, Embedded File Extractor, Picture Analyzer, Keyword Search, Email Parser, Encryption Detection, Interesting Files Identifier, Central Repository, PhotoRec Carver, Virtual Machine Extractor, YARA Analyzer, iOS Analyzer (iLEAPP). Both data sources completed ingest successfully.

**Step 4 — Artifact Examination**  
Systematically reviewed six artifact categories: Images/Videos, Documents, Email Messages, Web History, Web Search, and OS Accounts. Items bookmarked with tag "Jimmy Wilson." Metadata captured per item: file name, full path, created time, file size, and hash values.

**Step 5 — Report Generation**  
Generated Autopsy HTML report from all tagged items: E-Mail Messages (2), Tagged Files (5), Tagged Images (1), Tagged Results (19), Web History (7), Web Search (10). Formal examiner report submitted to HR using organizational template.

---

## Autopsy Report Summary

| Field | Value |
|---|---|
| Case | JimmyWilson |
| Examiner | Christopher Ham |
| Report Generated | 2026/06/01 12:18:23 |
| Data Sources | 2 (2020JimmyWilson.E01 + SYSTEM.vhd) |
| Tagged Files | 5 |
| Tagged Results | 19 |
| Email Messages | 2 |
| Web History (tagged) | 7 |
| Web Search (tagged) | 10 |

---

## Conclusions

1. **Pattern of criminal planning activity** — Searches for handguns, identity theft methods, fast getaway cars, and how to disappear without a trace across two browsers on two consecutive dates reflect deliberate, sustained research inconsistent with legitimate real estate duties.

2. **Personal email on corporate device** — Jimmy Wilson used personal Gmail (`wilsonjimmy807@gmail.com`) to communicate with `robert.ripoff@gmx.com` on a corporate workstation.

3. **Named contacts of concern** — Desktop files "Jose Badguy" and "Robert Ripoff" suggest the user maintained records on specific individuals. "Robert Ripoff" directly matches the email contact.

4. **File concealment activity** — Six extension mismatches and four encryption-suspected files indicate possible deliberate concealment of content.

5. **External storage use** — Nine USB devices were attached, indicating potential data exfiltration. Contents not determinable from the current image alone.

---

## Tools and Frameworks

**Tool:** Autopsy 4.22.1 (Sleuth Kit) · **Environment:** ProxMox VE / Windows 11 VM · **Format:** E01

- NIST SP 800-86 — Integrating Forensic Techniques into Incident Response
- NIST SP 800-61r2 — Computer Security Incident Handling Guide
- RFC 3227 — Guidelines for Evidence Collection and Archiving
- ACPO Good Practice Guide for Digital Evidence

---

## Skills Demonstrated

Disk Image Forensics (E01) · Autopsy Forensic Suite · Chain of Custody · Hash Verification (MD5/SHA-1) · Browser Artifact Recovery · Email Forensics · OS Account Analysis · Web History Reconstruction · Evidence Bookmarking · Extension Mismatch Analysis · Forensic Report Writing · Technical Writing for Non-Technical Audiences · Virtual Machine Forensics · Corporate Endpoint Investigation

---

## Repository Contents

| File | Description |
|---|---|
| `README.md` | This file — full lab documentation |
| `JimmyWilson_ForensicExamination_CHam_UofL.docx` | Completed assignment submission (instructor template) |

---

## Examiner

**Christopher Ham**  
CEH · CISM · SecurityX · Security+ · ECIH EC-Council Incident Handler · CCNA · Splunk Core Certified User · NCAE-C OSINT Specialist Investigator  

[LinkedIn](https://linkedin.com/in/christopher-ham-cyber) · [Portfolio](https://cham252.github.io) · Christopher.ham2@protonmail.com · Durham, NC
