# RabTech Task 2 — Authorized Lab Dossier

**Status: Four requested dossier components prepared. External reachability test completed on 2026-11-05; written authorization details remain unprovided and are not fabricated here.**

## Contents

1. `authorized-lab-assets.csv` — asset inventory and verification evidence.
2. `stride-register-and-data-flow.md` — STRIDE threat register with explicit P1/P2 mitigation priorities and lab-specific data-flow diagram.
3. `rules-of-engagement.md` — proposed scope, permitted/prohibited activity, stop conditions, evidence handling, and approval checklist.
4. `README.md` — this overview.

## Verified lab facts (2026-11-05)

- LAB-01: OWASP Juice Shop in Kali Linux under WSL2 on Windows 11.
- Local URL: `http://127.0.0.1:3000`, TCP port 3000. A local HTTP check returned `HTTP/1.1 200 OK`.
- SQLite file observed at `~/juice-shop/data/juiceshop.sqlite`.
- Application listener observed on `*:3000` (all interfaces), not loopback-only.
- WSL networking mode was mirrored; WSL firewall integration was enabled.
- WSL Hyper-V firewall was enabled; default inbound action was Block; loopback was enabled. Windows Firewall was enabled on Domain, Private, and Public profiles. Blocked-packet logging was enabled on all three profiles. No enabled inbound TCP allow rule for local port 3000 was found.
- **Separate-device reachability test:** From the small laptop (test device), `Test-NetConnection` to the big laptop (Juice Shop host), TCP port 3000, returned `TcpTestSucceeded: False` and `PingSucceeded: False`. A browser attempt to access the host's port 3000 did not load.
- **Firewall log evidence:** Windows Firewall recorded dropped ICMP and UDP traffic from the test device to the host. The UDP destination port was 137. A targeted search found no matching TCP/3000 DROP entry. Hyper-V firewall settings were reconfirmed as enabled, with default inbound action Block, outbound action Allow, and loopback enabled.
- **Interpretation:** The service was not reachable from the tested device during the test, and Windows Firewall demonstrably dropped some traffic from that device. However, the logs do not prove that Windows Firewall dropped the specific TCP/3000 connection. Wi-Fi client isolation, routing, Hyper-V firewall policy, or another network control may explain the failure. Do not claim universal network isolation.
- LAB-02 remains uninstalled/unverified and is not an approved target.
- Application log location/retention and database contents have not been verified.

## Authorization and limitations

This dossier is documentation, not permission to test. The lab owner, written approval reference/date, approved testing window, permitted tools/rate limits, emergency contact, and evidence-retention requirements remain pending unless separately supplied by RabTech/supervisor. Do not conduct security testing beyond explicitly authorized scope.

## Final handling

- The assessor's name is recorded in the Rules of Engagement.
- Do not invent supervisor approval or approval references.
- Redact personal and network identifiers before public sharing if RabTech does not require them in the submission.
