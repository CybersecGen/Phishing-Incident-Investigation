# Phishing Incident Investigation – Email Analysis & IOC Extraction


**Date:** 01-06-2025
**Environment:** Simulated Global Payments Provider SOC  
**Domain:** Email Security / Threat Detection / SOC Investigation  
**Focus:** Phishing analysis, IOC extraction, and detection engineering in a cloud-enabled SOC environment  

---

## 1. Incident Overview

A suspected phishing email was reported by an end user within the organization. The message impersonated a legitimate service provider and attempted to redirect the user to a credential harvesting page.

The objective of this investigation was to:

- Validate whether the email was malicious  
- Identify indicators of compromise (IOCs)  
- Assess potential user interaction risk  
- Recommend detection and response improvements within a SOC environment  

---

## 2. Threat Summary

The email leveraged common phishing techniques targeting financial environments, including social engineering and domain impersonation.

Observed characteristics:

- Domain spoofing of a trusted service provider  
- Urgency-based messaging to trigger immediate action  
- Credential harvesting via fake login portal  
- Use of HTTPS to increase perceived legitimacy  

---

## 3. Email Analysis

### 3.1 Sender Analysis

- Display name impersonated a legitimate internal service  
- Sender domain closely resembled a trusted corporate domain  
- Reply-To address did not match sender domain (spoofing indicator)  

---

### 3.2 Header Analysis
```text
SPF: FAIL
DKIM: FAIL
DMARC: FAIL or misaligned
```

- Email authentication checks failed or were inconsistent  
- Originating IP not associated with legitimate infrastructure  
- No known reputation history for business activity  

---

## 4. Payload & URL Analysis

The email contained an embedded link presented as a secure login portal.

Findings:

- Redirect chain led to a credential harvesting page  
- Domain used typosquatting techniques to mimic a trusted service  
- HTTPS certificate used to increase trust perception  
- Fake login page visually replicated a legitimate corporate portal  

---

## 5. Tools Used

- VirusTotal – URL and domain reputation analysis  
- MXToolbox – SPF/DKIM/DMARC validation and header inspection  
- URLVoid / PhishTank – phishing classification checks  
- WHOIS Lookup – domain registration and infrastructure analysis  

---

## 6. Indicators of Compromise (IOCs)

| IOC Type     | Value |
|--------------|-------|
| Domain       | secure-payments-login[.]com |
| IP Address   | 185.xx.xx.xx |
| Sender Email | support@secure-payments-login[.]com |
| URL Path     | /verify/account/login |

---

## 7. Investigation Workflow

- User reported suspicious email to SOC  
- Email headers and payload extracted for analysis  
- Authentication mechanisms (SPF/DKIM/DMARC) validated  
- External threat intelligence tools used for reputation checks  
- IOC correlation performed in simulated SIEM environment  
- Search conducted for additional affected users or similar emails  
- Assessed potential user interaction (click or credential submission simulation)  

---

## 8. Detection Gaps Identified

- No automated alerting for domain spoofing attempts  
- Lack of monitoring for SPF/DKIM/DMARC failures  
- Limited visibility into user interaction with phishing URLs  
- No detection rules for lookalike domains or typosquatting  

---

## 9. Detection & Response Improvements

### Email Security Enhancements

- Enforce strict SPF/DKIM/DMARC rejection policies  
- Implement advanced phishing detection rules in email gateway  
- Block newly registered or suspicious domains dynamically  

---

### SOC / SIEM Enhancements

- Create alerting for:
  - Domain impersonation patterns  
  - Email authentication failures  
  - Suspicious URL reputation changes  

- Integrate email telemetry into SIEM (e.g., Microsoft Sentinel)  
- Correlate phishing indicators with identity and sign-in logs  

---

### Incident Response Actions

- Block malicious domains and IP addresses  
- Add IOCs to threat intelligence feeds  
- Update email filtering rules  
- Strengthen user phishing awareness training  

---

## 10. Example Attack Flow (Simulated)

User receives phishing email  
→ Clicks malicious link  
→ Redirected to credential harvesting page  
→ Credentials submitted  
→ SOC validates indicators using threat intelligence tools  
→ Domain and IP are blocked across environment  

---

## 11. Key Takeaways

This investigation demonstrates how phishing attacks continue to exploit human behavior and weak email authentication controls.

From a cloud security engineering perspective, effective defense requires:

- Strong email authentication enforcement  
- SIEM-based correlation of identity + email signals  
- Threat intelligence integration  
- Automated detection of domain impersonation patterns  

Improving detection engineering and cloud security visibility significantly reduces time to detect and respond to credential-based attacks.
