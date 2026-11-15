# Web Application Security

## HTTP request anatomy

An HTTP request typically contains a method, path, protocol version, headers, and sometimes a body. Responses contain a status code, headers, and optional body.

Common methods: GET, POST, PUT, PATCH, DELETE, OPTIONS, HEAD.

Common status codes:
- 200 OK
- 301/302 redirect
- 400 bad request
- 401 unauthenticated
- 403 forbidden
- 404 not found
- 500 server error

## Important browser security concepts

- Cookies can use HttpOnly, Secure, and SameSite attributes.
- Sessions should use unpredictable identifiers and expire appropriately.
- Authentication and authorization must be enforced server-side.
- Input validation is not a substitute for context-aware output encoding or parameterized queries.
- TLS protects data in transit but does not fix application authorization flaws.

## Common vulnerability classes

- Broken access control / IDOR
- Injection (including SQL injection)
- Cross-site scripting (XSS)
- Cross-site request forgery (CSRF)
- Security misconfiguration
- Vulnerable and outdated components
- Authentication and session failures
- Server-side request forgery (SSRF)

## Burp Suite learning workflow

In a deliberately vulnerable local lab:
1. Configure the browser to proxy through Burp.
2. Intercept and inspect a request.
3. Send a copy to Repeater.
4. Change one parameter at a time.
5. Compare response status, headers, and body.
6. Document the impact and remediation.

Do not test public applications without explicit permission.

## Remediation principles

Use parameterized queries, server-side access checks, secure cookie attributes, output encoding, CSRF protections where appropriate, dependency updates, and secure defaults.

## Reference

- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [PortSwigger Web Security Academy](https://portswigger.net/web-security)
