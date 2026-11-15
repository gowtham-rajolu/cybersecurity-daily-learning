# SOC and SIEM Fundamentals

## SOC workflow

1. Collect telemetry from endpoints, identity systems, networks, and applications.
2. Normalize and enrich events.
3. Detect suspicious patterns.
4. Triage alerts using context and severity.
5. Investigate scope, timeline, and impact.
6. Contain and eradicate according to incident procedures.
7. Recover, document, and improve detections.

## Important log sources

- Authentication events and MFA outcomes
- Endpoint process and network telemetry
- DNS and proxy logs
- Firewall and VPN events
- Cloud audit logs
- Web server and application logs

## SIEM concepts

A SIEM centralizes and correlates security events. Learn parsing, field normalization, time synchronization, detection rules, dashboards, alert severity, retention, and false-positive tuning.

## Example investigation questions

- Which account or host generated the event?
- Is the source expected for this user and time?
- What happened immediately before and after?
- Are there related events on other systems?
- What evidence supports benign or malicious classification?
- What containment action is authorized?

## Mini-project idea

Build a small defensive log-analysis pipeline using sample logs: parse events, normalize timestamps, detect repeated failed logins, produce an alert with supporting evidence, and document false-positive cases. Use synthetic or sanitized data only.
