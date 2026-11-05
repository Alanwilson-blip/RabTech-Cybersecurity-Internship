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
- WSL Hyper-V firewall was enabled; default inbound action was Block; loopback was enabled. Windows Firewall was enabled on Domain, Private, and Public profiles. Windows Firewall blocked-packet logging was subsequently enabled on all three profiles. The enabled inbound TCP rule listing showed no allow rule for local port 3000.
- **Separate-device reachability test:** from the small laptop (`192.168.31.30`), `Test-NetConnection 192.168.31.106 -Port 3000` returned `TcpTestSucceeded: False` and `PingSucceeded: False`. A browser attempt to `http://192.168.31.106:3000` did not load. The big laptop hosting Juice Shop had IPv4 address `192.168.31.106`; the test was conducted while both devices were connected to the same Wi-Fi network.
- **Firewall log evidence:** after blocked-packet logging was enabled, `pfirewall.log` recorded `DROP ICMP` from `192.168.31.30` to `192.168.31.106` and `DROP UDP` from `192.168.31.30` to `192.168.31.106` on destination port 137. A targeted search found no matching TCP/3000 DROP entry. Hyper-V firewall settings were reconfirmed as `Enabled=True`, `DefaultInboundAction=Block`, `DefaultOutboundAction=Allow`, and `LoopbackEnabled=True`.
- **Interpretation:** the service was not reachable from the small laptop during this test, and Windows Firewall demonstrably dropped some traffic from that device. However, the logs do not prove that Windows Firewall dropped the specific TCP/3000 connection. Host/Hyper-V firewall policy, Wi-Fi client isolation, routing, or another network control may explain the failed application connection. Do not claim that the firewall alone caused the TCP/3000 block or that all possible network paths are proven isolated.
- LAB-02 remains uninstalled/unverified and is not an approved target.
- Application log location/retention and database contents have not been verified.

## Authorization and limitations
This dossier is documentation, not permission to test. The lab owner, written approval reference/date, approved testing window, permitted tools/rate limits, emergency contact, and evidence-retention requirements remain pending unless separately supplied by RabTech/supervisor. Do not conduct security testing beyond explicitly authorized scope.

## Final handling
- The assessor's name is to be completed by the assessor in the Rules of Engagement.
- Do not invent supervisor approval or approval references.
- Redact personal and network identifiers before public sharing if RabTech does not require them in the submission.
