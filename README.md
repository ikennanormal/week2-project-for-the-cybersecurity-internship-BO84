Letter of Authorization for Cybersecurity Testing Written Permission & Rules of Engagement — Phase 1 & Phase 2


 
Authorization Parameter

Reference No.

Date of Issue

Client / Target Owner

Authorized Tester (Intern)

Program / Batch

Authorization Valid
 
Engagement Specification

NW-LOA-B084-017

12 November 2026

Networkwalks (www.networkwalks.com)

Azubuike Divine Ikenna

B084 — Networkwalks Cybersecurity Internship

12 November 2026 to 19 November 2026
 


To Whom It May Concern,


This letter confirms that Networkwalks (the "Client") grants written permission to the authorized tester named above (Azubuike Divine Ikenna, Batch B084) to perform limited, non-destructive security testing against the systems listed in the scope below. This authorization is issued as part of the Networkwalks Cybersecurity Internship and is valid strictly for the dates stated above.

1. Scope of Authorization

The tester is authorized to perform reconnaissance and network scanning activities against the following targets only:

networkwalks.com — the Client's public website and its associated public DNS records.

192.168.89.0/24 — the tester's own local area network (LAN), owned and controlled by the tester.


Any system, domain, IP address, or network not listed above is strictly out of scope and must not be tested.

2. Authorized Activities

Only the following activities are permitted under this authorization (Phase 1 and Phase 2 of a penetration test):

Footprinting and reconnaissance using passive and light information-gathering tools ( whois, , , , , and ).
whatweb nslookup curl wafw00f dnsrecon

Network scanning and host discovery using Zenmap / Nmap against the tester's own local subnet ( 192.168.89.0/24).







Networkwalks | W2-PM-FINAL Report — Azubuike Divine Ikenna (Batch B084)	Page 1 of 12 
3. Prohibited Activities

Exploitation, gaining unauthorized access, or privilege escalation on any target system.

Denial-of-service (DoS), brute-force, password attacks, or any activity that could disrupt or degrade a service.
Accessing, copying, modifying, or deleting any data belonging to the Client or any third party.

Social engineering of Client staff or any testing outside the scope defined in Section 1.

4. Conditions & Governance

The tester must stop all testing immediately if asked to do so by the Client, or if any unexpected disruption occurs.
All findings and information discovered must be kept confidential and used exclusively for this internship report.
The tester acts responsibly and lawfully at all times and is solely responsible for any action taken outside this scope.
This authorization expires on the end date shown above and must be renewed in writing to remain valid.

5. Acknowledgement & Signatures

By signing below, the Client confirms it owns or controls the in-scope targets and authorizes the described testing, and the tester confirms they have read, understood, and will comply with the scope and conditions of this letter.

 
Authorized by (Client / Target)

Sonia John
Managing Director, Networkwalks


Signature & Date: 12 November 2026
 
Acknowledged by (Tester)

Azubuike Divine Ikenna Cybersecurity Intern, Batch B084


Signature & Date: 12 November 2026
 


W2-PM-FINAL | CYBERSECURITY & ETHICAL HACKING PROJECT REPORT
Penetration Testing Report: Footprinting & Network Scanning
Phase 1 (Reconnaissance) & Phase 2 (Network Discovery) Assessment



 
Report Field

Pentester Name

Program / Batch

Date of Assessment

Modules Completed
 
Assessment Record

Azubuike Divine Ikenna

B084 — Networkwalks Cybersecurity Internship

12 November 2026

W2-PM1 (Multiple Kali Tools) & W2-PM5 (Network Scanning with Zenmap)
 


Networkwalks | W2-PM-FINAL Report — Azubuike Divine Ikenna (Batch B084)	Page 2 of 12 
Report Field

Client / Target Scope



Permission Secured?

Phases Covered
 
Assessment Record

1. networkwalks.com (Written authorization secured)
2. Local LAN Subnet 192.168.89.0/24 (Tester-owned network)

Yes — Ref. NW-LOA-B084-017 (Attached)

Phase 1: Reconnaissance & Footprinting | Phase 2: Scanning & Network Discovery
 


1. LIABILITY DISCLAIMER


I, Azubuike Divine Ikenna, have performed these activities strictly on the systems and devices where I had secured written permission or on networks and devices that I own and control myself. All materials in this report are for authorized educational and research purposes only. Unauthorized access to computer systems is illegal in most jurisdictions even when no damage occurs, and misuse of these techniques can result in criminal prosecution, heavy fines, and permanent career consequences.


2. EXECUTIVE SUMMARY & INTRODUCTION

This report documents the practical execution and analytical findings of Week 2 of the Networkwalks Cybersecurity Internship (Batch B084). The assessment spans two foundational phases of ethical hacking: external reconnaissance and footprinting against networkwalks.com using six specialized Kali Linux utilities (Module W2-PM1), and internal network discovery across my local area network
192.168.89.0/24 using Zenmap (Module W2-PM5).


During external footprinting, passive and light-active queries successfully mapped the target's domain registration lock status, authoritative HostGator and DomainControl name servers, hosting IP address ( 192.232.216.135), application stack (Apache, WordPress 7.1.4, WordPress Download Manager 3.3.76, jQuery 3.7.1, Bootstrap 7.1.4), HTTP headers exposing /wp-json/, and active protection via ModSecurity (SpiderLabs) WAF.

During internal network scanning, a Zenmap/Nmap sweep of 256 IP addresses on 192.168.89.0/24 completed in 42.91 seconds and identified 30 live hosts. Several critical
infrastructure nodes and endpoints were discovered with exposed management and service ports— most notably unencrypted Telnet (TCP 23) and FTP (TCP 21) on the MikroTik gateway
( 192.168.89.1), Windows SMB/RPC services (TCP 135, 139, 445) on three hosts, and database ports (MySQL TCP 3306, PostgreSQL TCP 5432) on internal servers.













Networkwalks | W2-PM-FINAL Report — Azubuike Divine Ikenna (Batch B084)	Page 3 of 12 
3. METHODOLOGY & TOOLS USED

 
Tool / Utility

Kali Linux & Windows


whois


whatweb


nslookup


curl -I


wafw00f


dnsrecon


Zenmap (Nmap 7.993)
 
Phase

Environment


Phase 1 (W2-PM1)

Phase 1 (W2-PM1)

Phase 1 (W2-PM1)

Phase 1 (W2-PM1)

Phase 1 (W2-PM1)

Phase 1 (W2-PM1)

Phase 2 (W2-PM5)
 
Technical Purpose & Role in Assessment

Dual testing platforms used to execute Linux CLI reconnaissance tools and Windows GUI network mapping.

Queries registrar databases for domain creation/expiry dates, EPP lock codes, privacy proxy details, and name servers.

Fingerprints web server software, CMS platforms, plugins, JavaScript libraries, cookies, and redirect behavior.

Resolves the target domain name to its underlying IPv4 host address via public DNS resolvers.

Fetches raw HTTP response headers to inspect caching layers, cookie flags, security policies, and API link headers.

Sends crafted HTTP probes to detect and fingerprint Web Application Firewalls protecting the target site.

Performs comprehensive DNS enumeration across SOA, NS, BIND version, MX, TXT (SPF/verification), and SRV records.

Discovers live hosts on the 192.168.89.0/24 subnet, enumerates open TCP ports, identifies MAC OUI vendors, and generates topology maps.
 


4. ACTIVITIES PERFORMED & TECHNICAL FINDINGS

4.1 Phase 1: External Footprinting & Reconnaissance (W2-PM1)

Six sequential reconnaissance techniques were executed from Kali Linux against networkwalks.com on 11–12 November 2026:

Domain Registration Intelligence ( whois networkwalks.com): Confirmed registration through GoDaddy.com, LLC (IANA ID 146), created on 2019-11-06 and valid until 2027-11-06. Registrant contact details are shielded by Domains By Proxy, LLC (Tempe, Arizona). All four ICANN EPP client locks ( clientDeleteProhibited, clientRenewProhibited,
clientTransferProhibited, clientUpdateProhibited) are active, though DNSSEC is marked unsigned. Authoritative name servers listed include NS6135.HOSTGATOR.COM, NS6136.HOSTGATOR.COM, NS29.DOMAINCONTROL.COM, and NS30.DOMAINCONTROL.COM.
Web Stack Fingerprinting ( whatweb networkwalks.com): Initial HTTP requests return a 301 Moved Permanently redirect to HTTPS. The HTTPS endpoint ( 200 OK) runs on Apache in the United States ( 192.232.216.135) and is powered by WordPress 7.1.4, WordPress Download Manager 3.3.76, Bootstrap 7.1.4, and jQuery 3.7.1. It also exposed the administrative contact email info@networkwalks.com and sets an HttpOnly session cookie ( __wpdm_client).
DNS Host Resolution ( nslookup networkwalks.com): Queried via Google Public DNS ( 8.8.8.8#53), resolving networkwalks.com to IPv4 address 192.232.216.135.
HTTP Header Inspection ( curl -I https://networkwalks.com): Returned HTTP/1.1 200 OK from Apache with X-nginx-cache: WordPress and X-Endurance-Cache-Level: 0. The Link header explicitly advertises the WordPress REST API root ( <https://networkwalks.com/wp-json/>) and page endpoint ( /wp-json/wp/v2/pages/53).


Networkwalks | W2-PM-FINAL Report — Azubuike Divine Ikenna (Batch B084)	Page 4 of 12 
WAF Fingerprinting ( wafw00f networkwalks.com): Completed in 2 requests and confirmed that https://networkwalks.com is actively protected behind ModSecurity (SpiderLabs) WAF.
DNS Record Enumeration ( dnsrecon -d networkwalks.com): Identified SOA record ns6135.hostgator.com ( 50.87.144.87) and NS record ns6136.hostgator.com
( 192.232.216.131), both disclosing BIND version "9.16.23-RH". Enumerated mail exchange mail.networkwalks.com ( 192.232.216.135), SPF policy v=spf1 +a +mx +ip4:50.87.144.87
+include:websitewelcome.com ~all, a Google site verification TXT token, and 8 cPanel autodiscover SRV records ( _autodiscover._tcp.networkwalks.com) on port 443.

4.2 Phase 2: Local Network Scanning with Zenmap (W2-PM5)

Using Zenmap (Nmap 7.993) on 12 November 2026 at 13:54 (+0100), I scanned my local subnet 192.168.89.0/24 across all 256 IPv4 addresses. The scan completed in 42.91 seconds and
identified exactly 30 live hosts. Out of the 30 active nodes, 11 hosts exposed open TCP services, 1 host responded with a filtered echo port, and 18 hosts had all 100 scanned ports in closed (reset) or filtered (no-response) states.

 
IP Address


192.168.89.1



192.168.89.20


192.168.89.40


192.168.89.43

192.168.89.44


192.168.89.47

192.168.89.51

192.168.89.53

192.168.89.56


192.168.89.57


192.168.89.63


192.168.89.64


192.168.89.66


192.168.89.67

192.168.89.76
 
MAC Address


F4:1E:57:73:60:FE



2C:8D:B1:9C:54:28


18:3D:A2:55:36:C4


EE:9B:8D:D9:AA:6B

2E:B6:CD:91:66:BC


4E:40:7F:42:1A:6B

78:A7:5A:A8:27:E8

6A:CA:1C:9C:DC:20

70:A8:D3:3F:8E:96


28:11:A8:10:99:65


2A:FE:5E:37:D0:8B


58:96:71:B2:4C:EE


18:3D:A2:8F:B9:84


D6:3A:58:9A:F6:AF

66:16:AB:F0:D5:E2
 
Hardware Vendor


Routerboard.com


Intel Corporate


Intel Corporate


Unknown

Unknown


Unknown

Unknown

Unknown

Intel Corporate


Intel Corporate


Unknown


WNC


Intel Corporate


Unknown

Unknown
 
Latency


0.022s


0.098s


0.22s


0.026s

0.022s


0.053s

0.015s

0.012s

0.066s


0.056s


0.28s


0.067s


0.26s


0.023s

0.016s
 
Open / Filtered Ports & State

Open: 21/ftp, 22/ssh, 23/telnet, 80/http, 2000/cisco-sccp

100 filtered ports (no-response)

100 filtered ports (no-response)

Open: 8081/blackice-icecap

Open: 5000/upnp, 49152/unknown

100 closed ports (reset)

100 closed ports (reset)

100 closed ports (reset)

100 filtered ports (no-response)

100 filtered ports (no-response)

100 filtered ports (no-response)

100 filtered ports (no-response)

100 filtered ports (no-response)

Open: 49152/unknown

100 closed ports (reset)
 



Networkwalks | W2-PM-FINAL Report — Azubuike Divine Ikenna (Batch B084)	Page 5 of 12 
IP Address


192.168.89.77



192.168.89.78


192.168.89.81

192.168.89.83



192.168.89.88



192.168.89.95

192.168.89.105



192.168.89.106


192.168.89.121


192.168.89.122


192.168.89.123

192.168.89.127

192.168.89.252


192.168.89.253

192.168.89.254
 
MAC Address


C4:75:AB:FF:AA:AF



8C:8B:5B:8F:FE:A5


56:3D:29:E0:29:34

06:06:3B:8D:B5:AC



58:96:71:B2:A4:26



CE:5A:7D:83:78:AA

Localhost (Scanner)



70:32:17:D7:1D:B0


62:7D:4D:AA:2C:9A


E6:18:C9:B0:77:B9


70:52:D8:3D:E5:12

EC:7E:91:AA:0C:05

78:45:58:A2:62:87


D8:B3:70:C3:AA:83

28:70:4E:B0:1C:A2
 
Hardware Vendor

Intel Corporate



WNC


Unknown

Unknown


WNC


Unknown

Local Interface


Intel Corporate


Unknown


Unknown


Itel Mobile Limited

Itel Mobile Limited

Ubiquiti


Ubiquiti

Ubiquiti
 
Latency


0.030s



0.32s


0.022s

0.018s


0.082s


0.036s

0.00099s


0.071s


0.020s


0.41s


0.090s

0.078s

0.027s


0.0095s

0.016s
 
Open / Filtered Ports & State

Open: 135/msrpc, 139/netbios-ssn, 445/microsoft-ds, 5357/wsdapi

100 filtered ports (no-response)

100 closed ports (reset)

Open: 80/http, 443/https, 3000/ppp, 3306/mysql, 5000/upnp, 5432/postgresql

Open: 135/msrpc, 139/netbios-ssn, 445/microsoft-ds

100 closed ports (reset)

Open: 135/msrpc, 139/netbios-ssn, 445/microsoft-ds

100 filtered ports (no-response)

Open: 5000/upnp, 5432/postgresql

Filtered: 7/echo (99 closed ports)

100 closed ports (reset)

100 closed ports (reset)

Open: 22/ssh, 80/http, 443/https

Open: 22/ssh

Open: 22/ssh, 80/http, 443/https
 


5. COMPREHENSIVE RISK ANALYSIS & IMPACT ASSESSMENT

Combining external reconnaissance of networkwalks.com and internal discovery of 192.168.89.0/24 reveals distinct security observations across both environments:

 
#	Security Finding

1	Cleartext Management Protocols on Gateway
 
Technical Evidence

192.168.89.1 (Routerboard.com) exposes TCP 21 (FTP), TCP 23 (Telnet), and TCP 80 (HTTP).
 
Potential Security Impact

Credentials and administrative traffic transmitted in cleartext can be intercepted via network sniffing.
 
Severity

High
 







Networkwalks | W2-PM-FINAL Report — Azubuike Divine Ikenna (Batch B084)	Page 6 of 12 
#	Security Finding

2	Exposed Database & UPnP Services on LAN




3	Internal SMB / NetBIOS File Sharing Exposure



4	CMS & Plugin Version Disclosure



5	DNS Infrastructure & BIND Version Leakage



6	Direct Origin IP & REST API Endpoint Visibility



7	WAF Fingerprinting (ModSecurity)
 
Technical Evidence

192.168.89.83 exposes MySQL (3306), PostgreSQL (5432), and UPnP (5000);
192.168.89.121 exposes PostgreSQL & UPnP.

Hosts .77, .88, and .105 expose TCP 135 (MSRPC), 139 (NetBIOS), and 445 (SMB).


whatweb identified WordPress 7.1.4 and WP Download Manager 3.3.76 on networkwalks.com.


dnsrecon exposed BIND 9.16.23-RH on HostGator NS
servers, SPF IP ranges, and DNSSEC: unsigned.


nslookup resolved origin IP 192.232.216.135; curl -I
exposed /wp-json/ and Apache server banner.

wafw00f identified ModSecurity (SpiderLabs) WAF on
https://networkwalks.com.
 
Potential Security Impact

Direct network exposure of database engines increases risk of unauthorized queries, brute-force, or UPnP port forwarding abuse.

Enables lateral movement, SMB relay attacks, or enumeration of unauthenticated network shares.

Allows attackers to map exact software builds against public CVE databases for targeted exploitation.

Reveals exact DNS daemon versions and leaves domain queries vulnerable to DNS spoofing without DNSSEC.

Facilitates user enumeration via WordPress REST API and direct origin targeting.

While ModSecurity provides strong active defense, identifying the exact WAF informs evasion crafting.
 
Severity

High





Medium




Medium




Medium




Low




Low
 


Note: All findings above reflect non-intrusive reconnaissance and port enumeration observations under authorized scope. No exploitation or credential testing was attempted.

6. ACTIONABLE SECURITY RECOMMENDATIONS

Disable Cleartext Protocols on RouterOS ( 192.168.89.1): Immediately disable Telnet (TCP 23), FTP (TCP 21), and unencrypted HTTP (TCP 80) management interfaces on the MikroTik gateway; enforce SSH (TCP 22) with key-based authentication and HTTPS.
Restrict Database & UPnP Bindings ( 192.168.89.83 & .121): Bind MySQL (3306) and PostgreSQL (5432) exclusively to 127.0.0.1 or trusted application subnets via host firewall rules, and disable UPnP (TCP 5000) unless strictly required.
Harden Windows SMB/RPC Endpoints ( .77, .88, .105): Enforce SMB signing, disable legacy SMBv1/NetBIOS over TCP/IP, and restrict ports 135, 139, and 445 using Windows Defender Firewall.
Minimize CMS & HTTP Header Fingerprinting ( networkwalks.com): Strip WordPress generator meta tags and plugin version strings from public HTML, restrict unauthenticated access to sensitive /wp-json/wp/v2/users endpoints, and suppress detailed server banners.



Harden DNS Configuration: Enable DNSSEC at the registrar/DNS provider level, hide BIND software version strings ( version "none"; in named.conf), and consolidate legacy vs. active name server records.
Maintain ModSecurity WAF & Periodic LAN Audits: Keep ModSecurity OWASP Core Rule Set (CRS) rules updated and conduct scheduled Zenmap discovery sweeps to detect rogue or randomized-MAC devices on the local LAN.

7. CONCLUSION

During Week 2 of the Networkwalks Cybersecurity Internship (Batch B084), I successfully completed both external domain reconnaissance (W2-PM1) and internal network discovery (W2-PM5). By combining six Kali Linux footprinting utilities with Zenmap network scanning and topology mapping, I demonstrated how passive and active intelligence gathering uncovers critical architectural details, software versions, and exposed network services.

This engagement underscored the importance of layered defense: while networkwalks.com benefits from HTTPS enforcement, ICANN registrar locks, and ModSecurity WAF protection, reducing metadata leakage and enabling DNSSEC will further harden its external posture. Internally, remediating cleartext gateway protocols and restricting exposed database and SMB ports on
192.168.89.0/24 will significantly reduce the local attack surface.






9. TECHNICAL EVIDENCE & ARTIFACTS COLLECTED

9.1 Phase 1: Kali Linux Reconnaissance Screenshots (W2-PM1)


CURL



























































































































THE IMAGE OF THE ZENMAP TOPOLOGY












