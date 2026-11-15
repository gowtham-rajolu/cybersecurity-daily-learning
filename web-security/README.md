# Web application security notes

I'm using these notes alongside the guided web labs. I want to get used to reading the request and response first, before jumping to a vulnerability name.

## HTTP request and response

A request normally has a method, path, protocol version, headers and sometimes a body. The server sends back a status code, headers and usually a response body.

Methods I should recognise: GET, POST, PUT, PATCH, DELETE, OPTIONS and HEAD.

Status codes I keep seeing:

- 200 — request succeeded
- 301/302 — redirect
- 400 — bad request
- 401 — authentication is required or failed
- 403 — request understood but access denied
- 404 — resource not found
- 500 — server-side error

## Browser and session points

- `HttpOnly` stops normal browser JavaScript from reading a cookie.
- `Secure` tells the browser to send the cookie over HTTPS.
- `SameSite` affects when cookies are sent with cross-site requests.
- Session IDs should be hard to guess and should expire.
- The server must check authorization on every sensitive action.

HTTPS protects traffic in transit. It doesn't fix a server-side access-control bug.

## Vulnerability names to learn

- Broken access control / IDOR
- SQL and other injection
- Cross-site scripting (XSS)
- Cross-site request forgery (CSRF)
- Security misconfiguration
- Weak authentication or session handling
- Server-side request forgery (SSRF)
- Outdated or vulnerable dependencies

## Burp practice flow

In a deliberately vulnerable lab:

1. Set the browser proxy to Burp.
2. Intercept a request and read the headers and parameters.
3. Send it to Repeater.
4. Change one thing at a time.
5. Compare the response status, headers and body.
6. Write down what changed and why it matters.

I was also looking at an admin file-upload page in a guided lab. The important question isn't only whether a file uploads; I need to understand how the server validates it, where it stores it and whether the server can execute it.

## Fixes to remember

Use parameterised queries, enforce access checks on the server, encode output for its context, protect state-changing requests against CSRF where relevant, and keep dependencies updated.

Practise only against my own application or a lab that explicitly permits testing.

## Reference

- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [PortSwigger Web Security Academy](https://portswigger.net/web-security)
