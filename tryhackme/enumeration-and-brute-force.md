# Enumeration & Brute Force

**Platform:** TryHackMe  
**Date worked:** 24 November 2026  
**Status:** Completed practice session

## What I practised

This room focused on web application enumeration and testing a password-reset flow that used a short numerical token.

- Used Python's `requests` library to send HTTP requests.
- Added the `PHPSESSID` session cookie to requests so the server could associate requests with the current web session.
- Iterated through zero-padded three-digit candidates (for example, `000`, `001`, `002`) and inspected the server responses.
- Distinguished ordinary invalid-token responses from the successful response.
- Inspected the returned HTML and identified the success messages without copying credentials into this repository.

## Python notes

A session is useful when several requests need to share cookies:

```python
import requests

session = requests.Session()
session.cookies.set("PHPSESSID", "YOUR_SESSION_ID")

response = session.get("http://TARGET/")
print(response.status_code)
print(response.text)
```

For a form submission, preserve the same `session` object and send the form fields with `session.post(...)`. Match the parameter names, request method, headers and CSRF-token handling used by the actual application.

## What I learned

- A browser session cookie can be supplied through `requests.Session().cookies`.
- Zero-padding matters when a token is represented as a fixed-width string: use `f"{number:03d}"` to format values from `000` through `999`.
- HTTP status alone may not tell whether an attempt succeeded. Inspect response content and look for reliable application-level indicators.
- A successful response may contain sensitive information. Avoid printing or committing passwords, session IDs, reset tokens or flags.

## Security observations

A three-digit reset token has only 1,000 possible values and is vulnerable to guessing if the application does not enforce effective protections.

Defensive controls include:
- Generate reset tokens with a cryptographically secure random generator and sufficient entropy.
- Enforce short expiry and one-time use.
- Rate-limit attempts per account and source, with monitoring and alerting.
- Avoid revealing whether an account exists or whether a particular token guess is close.
- Invalidate outstanding reset tokens after a successful password reset.

## Follow-up practice

- [ ] Review how to inspect form fields and hidden CSRF tokens.
- [ ] Practise extracting specific HTML elements with Beautiful Soup.
- [ ] Compare response status, length and message content to build reliable success detection.
- [ ] Review secure password-reset design and rate-limiting.

## Sensitive-data handling

Credentials, the PHP session ID, reset-token values, target-specific details and the room flag are intentionally omitted from this public write-up.
