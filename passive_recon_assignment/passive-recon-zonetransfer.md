# Passive Reconnaissance — Practical Assignment

**Author:** Siddhesh Anil Yedge  
**Scope:** Passive techniques only. Test target: zonetransfer.me (authorized test domain).  
**Goal:** Map public attack surface and extract high-value, responsibly-disclosable findings.

---

## Tools & Methods
**CLI Tools:** host, whatweb, curl, dig, whois, dnsrecon, wafw00f, theHarvester, subfinder  
**Web / OSINT Sources:** BuiltWith, Wappalyzer, Netcraft, DNSDumpster, Google (GHDB), Have I Been Pwned, GitHub  

---

## Practical Example
**Sanitized output of fingerprinting:**
http://hackersploit.org  [301 Moved Permanently] HTTPServer: cloudflare, IP: 172.67.202.X
http://hackersploit.org [403 Forbidden] HTTPServer: cloudflare, PoweredBy: LiteSpeed


**Explanation:** Tools identify server software, HTTP headers, and IPs. Provides leads for further assessment.

---

## Findings & Insights

### 1) Tech Fingerprint
- **Evidence:** PHP 7.4.x, Apache 2.4.x (sanitized)  
- **Pentester POV:** Legacy versions have known CVEs; could be exploited in lab setups.  
- **Defender POV:** Upgrade software, apply patches, and harden server configurations.

### 2) DNS Records
- **A Record:** 5.196.105.X  
- **AAAA Record:** 64:ff9b::5c4:690e  
- **NS:** nsztm1.digi.ninja, nsztm2.digi.ninja  
- **MX:** Google MX records  
- **TXT:** google-site-verification=[redacted]  
**Pentester POV:** DNS reveals hosting, mail routing, and potential subdomains.  
**Defender POV:** Minimize public records and monitor DNS changes.

### 3) Subdomain Enumeration
- **Examples:** staging[target], vpn[target], owa[target], email[target], deadbeef[target]  
**Pentester POV:** Non-production subdomains can be weaker points.  
**Defender POV:** Remove stale subdomains and protect management endpoints with MFA & IP ACLs.

### 4) WAF Detection
- **Result:** No WAF detected (7 requests)  
**Pentester POV:** Indicates baseline filtering is absent.  
**Defender POV:** Consider WAF/IDS for automated probes.

### 5) Email Harvesting
- **Found (sanitized):** customer-service[at]example, pippa[at]example  
**Pentester POV:** Harvested emails could be used for phishing if breached elsewhere.  
**Defender POV:** Monitor exposed emails and enforce MFA.

---

## Conclusion & Next Steps
**Key Lessons Learned:**
1. Fingerprinting tools provide leads but require validation and CVE mapping.  
2. DNS & CT logs reveal hidden assets beyond the main site.  
3. Passive recon yields high-value data (subdomains, emails) when aggregated.

**Next Steps:**
- Complete subdomain validation using automation scripts.  
- Aggregate theHarvester output with proxies for larger coverage.  
- Build a lab to test CVE applicability safely.

---

**Responsible Disclosure Notice:** All findings are sanitized. Passive recon was conducted only on zonetransfer.me (authorized test target). No real PII or exploitable vulnerabilities are disclosed.

