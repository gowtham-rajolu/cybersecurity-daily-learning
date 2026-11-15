# SOC and SIEM — notes to work through

I want to understand the defensive side as well as pentesting. A SOC analyst needs to work out whether an alert is meaningful, what happened and what evidence supports the decision.

## Rough incident workflow

1. Collect events from endpoints, identity systems, networks and applications.
2. Put events into a format that can be searched together.
3. Look for suspicious patterns.
4. Triage alerts and check context.
5. Build a timeline and work out which accounts or machines are involved.
6. Follow the organisation's containment and response process.
7. Record what happened and what could be improved.

## Logs worth learning to read

- Authentication successes and failures
- Endpoint process creation and network connections
- DNS and proxy activity
- Firewall and VPN events
- Cloud audit events
- Web server and application logs

## What a SIEM does

A SIEM brings security events into one place so they can be searched and correlated. The parts I need to learn include parsing, normalising fields, time zones, detection rules, alert severity, dashboards and false-positive tuning.

## Questions I'd ask when an alert fires

- Which user or host generated it?
- Is the activity normal for that user and time?
- What happened just before and after the event?
- Are there related events on other machines?
- What evidence makes this look malicious or benign?
- What response actions am I allowed to take?

## Small project idea

Use synthetic or sanitised logs and write a Python script that finds repeated failed logins. For each alert, show the source, time range and matching log lines. Then test a few normal cases to see where the rule creates false positives.

I haven't built this pipeline yet. This is a project I want to try after I get more comfortable reading logs.
