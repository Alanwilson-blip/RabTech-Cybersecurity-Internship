# RabTech Task 2 — Authorized Lab Dossier

**Status:** Four dossier components prepared. External reachability testing was completed on 2026-11-05. Written authorization details have not been provided and are not fabricated in this dossier.

## Contents

1. `authorized-lab-assets.csv` — asset inventory and verification evidence.
2. `stride-register-and-data-flow.md` — STRIDE threat register, analyst-assigned mitigation priorities, trust boundaries and lab-specific data-flow diagram.
3. `rules-of-engagement.md` — proposed assessment scope, testing boundaries, stop conditions, evidence handling and approval checklist.
4. `README.md` — this overview.

## Verified Lab Facts (2026-11-05)

- **LAB-01:** OWASP Juice Shop running in Kali Linux under WSL2 on Windows 11.
- **Local URL:** `http://127.0.0.1:3000`, TCP port 3000. A local HTTP check returned `HTTP/1.1 200 OK`.
- **Database file:** Observed at `~/juice-shop/data/juiceshop.sqlite`.
- **Network listener:** Application listener observed on `*:3000`, not loopback-only.
- **WSL networking:** Mirrored networking mode was observed, with WSL firewall integration enabled.
- **Firewall configuration:** WSL Hyper-V firewall was enabled, with default inbound action Block and loopback enabled. Windows Firewall was enabled on Domain, Private and Public profiles. Blocked-packet logging was enabled on all three profiles. No enabled inbound TCP allow rule for local port 3000 was found.

### Separate-device reachability test

From the small laptop (test device), `Test-NetConnection` to the big laptop (Juice Shop host), TCP port 3000, returned:

- `TcpTestSucceeded: False`
- `PingSucceeded: False`

A browser attempt to access the host's port 3000 also failed.

### Firewall log evidence

- Windows Firewall recorded dropped ICMP and UDP traffic from the test device to the host.
- The UDP destination port was 137.
- A targeted search found no matching TCP/3000 DROP entry.
- Hyper-V firewall settings were reconfirmed as enabled, with default inbound action Block, outbound action Allow and loopback enabled.

**Interpretation:** The service was not reachable from the tested device during the test, and Windows Firewall demonstrably dropped some traffic from that device. However, the logs do not prove that Windows Firewall dropped the specific TCP/3000 connection. Wi-Fi client isolation, routing, Hyper-V firewall policy or another network control may explain the failure. Universal network isolation has not been established.

### Outstanding verification

- LAB-02, the deliberately vulnerable VM, remains uninstalled and unverified. It is excluded from the assessment scope.
- Application log location and retention have not been verified.
- Database contents have not been inspected; do not assume all records are synthetic.

## Authorization and Limitations

This dossier documents the training environment and preliminary security assessment. It is not permission to conduct security testing.

The following authorization details remain pending unless separately supplied by RabTech or the supervisor:

- Lab owner and written approval reference/date.
- Approved testing window.
- Permitted tools and request-rate limits.
- Emergency contact.
- Evidence-retention requirements.

Do not conduct security testing beyond explicitly authorized scope.

## Final Handling

- The assessor's name is recorded in the Rules of Engagement.
- Supervisor approval and authorization references have not been invented.
- Personal and network identifiers should be redacted before public sharing unless RabTech explicitly requires them for submission.
- Do not publish credentials, tokens, sensitive configuration or unredacted personal data.
