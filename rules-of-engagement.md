# Authorized Security Lab — Rules of Engagement

**Status: DRAFT — NOT AUTHORIZATION TO TEST**

This document defines a proposed, low-impact assessment scope for the local OWASP Juice Shop training instance. It does not grant permission to test. Written approval from the relevant lab owner/supervisor is required before security testing begins.

## 1. Parties and authorization

- Assessor: Alfiya Anjum .A
- Lab owner / approving representative: **PENDING RabTech/supervisor confirmation**
- Proposed asset: **LAB-01 — OWASP Juice Shop in Kali Linux under WSL2**
- Local URL verified: `http://127.0.0.1:3000`
- Approval reference and date: **PENDING**
- Approved asset list: only assets explicitly named in the supervisor-approved final inventory.
- Authorization rule: a locally running application and this draft document are not proof of authorization.

## 2. Environment and network protection evidence

- Juice Shop returned `HTTP/1.1 200 OK` at `127.0.0.1:3000` on 2026-11-05.
- The service was observed listening on `*:3000`.
- WSL configuration: `networkingMode=mirrored`, `firewall=true`.
- WSL Hyper-V firewall settings: `Enabled=True`, `DefaultInboundAction=Block`, `LoopbackEnabled=True`.
- The enabled inbound TCP rule listing showed no allow rule for local port 3000.
- Windows Firewall was enabled for Domain, Private, and Public profiles. Blocked-packet logging was enabled (`LogBlocked=True`) on all three profiles for the follow-up test.
- A separate-device test was performed on 2026-11-05 while both laptops were connected to the same Wi-Fi: the small laptop (`192.168.31.30`) ran `Test-NetConnection 192.168.31.106 -Port 3000`, which returned `TcpTestSucceeded: False` and `PingSucceeded: False`. A browser attempt to `http://192.168.31.106:3000` did not load.
- Windows Firewall log evidence: `pfirewall.log` recorded dropped ICMP traffic from `192.168.31.30` to `192.168.31.106` and dropped UDP traffic from that source to that destination on port 137. A targeted search found no matching TCP/3000 DROP entry. Hyper-V firewall settings were reconfirmed as enabled, with default inbound action Block, outbound action Allow, and loopback enabled.
- **Interpretation and limitation:** Juice Shop was not reachable from the tested second laptop at the time of testing, and Windows Firewall did drop some traffic from that device. The available log does not prove that Windows Firewall dropped the specific TCP/3000 connection. Wi-Fi client isolation, routing, Hyper-V policy, or another network control may also explain the failed application connection. The listener remains bound to `*:3000`; do not describe it as loopback-only or claim universal isolation.
- Application log location and retention have not been verified.
- LAB-02 (deliberately vulnerable VM) is not installed or verified and is excluded.

## 3. Proposed permitted activity (only after written approval)

Subject to explicit approval of each item:
- Confirm local service availability.
- Review application responses and documented routes using benign requests.
- Perform manual input-validation and access-control checks using synthetic accounts and data.
- Capture minimal evidence needed for the report.
- Record findings, limitations, and remediation recommendations.

Automated scanners, Nmap scans, proxy tools, fuzzing, authenticated testing, and tests that modify application data require explicit approval before use.

## 4. Prohibited activity

- Denial-of-service, stress, or load testing.
- Destructive payloads or actions likely to damage data or the host.
- Persistence, malware, credential theft, or credential reuse.
- Testing college networks, public systems, employer systems, home routers, third-party services, or any unlisted host.
- Scanning beyond the explicitly approved target and time window.
- Accessing, copying, or extracting real personal data, secrets, or unrelated files.
- Publishing evidence containing IP addresses, credentials, cookies, tokens, personal data, or other sensitive details.
- Any activity not explicitly authorized in writing.

## 5. Testing window, contacts, and stop conditions

- Approved start/end date and time: **PENDING**
- Permitted tools and rate limits: **PENDING**
- Emergency contact and escalation channel: **PENDING**
- Evidence retention/deletion date: **PENDING**

Stop immediately if traffic reaches an unapproved host, the service becomes unstable, real personal data or secrets appear, network exposure or target ownership is unclear, or the supervisor requests a stop. After stopping, cease testing, preserve only minimal relevant evidence, and notify the supervisor.

## 6. Evidence handling

- Store evidence in a private folder with access limited to the assessor and authorized supervisor.
- Use synthetic accounts and data only.
- Redact passwords, tokens, cookies, personal data, and unnecessary network identifiers.
- Do not publish raw packet captures or sensitive evidence publicly.
- Record date/time, asset ID, activity, result, and evidence filename.
- Follow the retention/deletion date provided by the supervisor.

## 7. Reporting

For each finding, record the finding ID and timestamp, verified asset and affected component, description and severity rationale, safe reproduction steps using synthetic data, impact and limitations, minimal redacted evidence, recommended remediation, and retest status.

## 8. Approval checklist

- [ ] RabTech/supervisor has confirmed the lab owner and provided written permission.
- [ ] The exact target and approved assets are listed in the final inventory.
- [x] WSL Hyper-V firewall default inbound-block policy and local loopback access have been documented.
- [x] Separate-device reachability test performed: TCP connection and browser access from the small laptop failed on 2026-11-05. Windows Firewall logs show dropped ICMP and UDP traffic from that laptop, but no TCP/3000 DROP entry; the specific blocking mechanism remains unconfirmed.
- [ ] Permitted tools, rate limits, and testing window are agreed.
- [ ] Emergency contact and escalation channel are recorded.
- [ ] Evidence retention/deletion requirements are agreed.
- [ ] Supervisor approval is recorded before testing begins.

**Final reminder:** This is a draft Rules of Engagement document, not authorization. Do not conduct further security testing until the supervisor has approved the final scope in writing.
