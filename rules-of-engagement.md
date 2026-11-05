# Rules of Engagement (RoE)

## 1. Assessment Details

- **Internship:** RabTech Cybersecurity Internship
- **Task:** Task 2 – Authorized Lab Dossier
- **Assessor:** Alfiya Anjum .A
- **Assessment date:** 5 November 2026

## 2. Objective

The objective is to document the authorized training environment, identify potential security threats, and define safe testing boundaries for the lab.

## 3. Authorized Scope

| Asset | Description | Scope |
|---|---|---|
| LAB-01 | OWASP Juice Shop running locally in Kali Linux under WSL2 | Local application assessment only |
| LAB-02 | Deliberately vulnerable VM | Excluded — not installed or verified |

The Juice Shop application was locally accessible at `http://127.0.0.1:3000`.

No testing of public websites, third-party systems, or devices without explicit permission is authorized.

## 4. Testing Boundaries

- Restrict testing to the locally installed Juice Shop application.
- Do not perform denial-of-service testing.
- Do not attack external systems or other devices.
- Do not access, modify, or disclose real user data.
- Do not attempt persistence, privilege escalation on the host, or destructive actions.
- Stop testing if unexpected impact occurs.

## 5. Connectivity Verification

A separate-device connectivity test was performed on 5 November 2026.

- The small laptop (test device) attempted to access the big laptop (Juice Shop host) on TCP port 3000.
- The TCP connection test failed.
- Browser access to the host's Juice Shop address also failed.
- Windows Firewall logs showed dropped ICMP and UDP traffic from the test device.
- No TCP port 3000 DROP entry was identified in the inspected log.

**Conclusion:** The application was not reachable from the tested second device during this test. The exact reason for the failed TCP connection was not established. This does not prove that every possible network path is isolated.

## 6. Safety and Data Handling

- Use only test data.
- Keep the lab environment separate from production systems.
- Do not publish credentials, tokens, database contents, or sensitive configuration.
- Redact personal and network identifiers before public sharing unless their disclosure is explicitly required.

## 7. Approval and Authorization

This document records the proposed scope and testing boundaries for the training lab. It is not, by itself, authorization to test systems outside the stated scope.

- **Assessor approval:** Pending
- **Supervisor approval:** Pending
- **Approval date:** Pending

Testing beyond the locally installed Juice Shop must not begin without explicit written authorization.

## 8. Final Declaration

The assessment is limited to the documented training environment. Any expansion of scope requires prior approval from the responsible authority.
