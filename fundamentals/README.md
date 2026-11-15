# Cybersecurity fundamentals — revision notes

These are the basic terms I want to be able to explain without memorising a definition.

## CIA triad

- **Confidentiality:** only the right people should see the data. Example: access controls on a user record.
- **Integrity:** data should not be changed without permission. Example: checking a file hash after transfer.
- **Availability:** systems should be usable when needed. Example: backups and recovery plans.

I need to remember that security is not only about stopping hackers. A system can have good confidentiality but still fail if nobody can access it when required.

## Terms I keep mixing up

| Term | My short version |
|---|---|
| Asset | Something worth protecting |
| Threat | Something that could cause harm |
| Vulnerability | A weakness |
| Exploit | A way of taking advantage of a weakness |
| Risk | The chance and impact of something going wrong |
| Control | A measure used to reduce risk |

Authentication is checking who someone is. Authorization is checking what that identity is allowed to do. Logging/auditing records what happened.

## Defense in depth

Don't depend on one control. For example, a server can use MFA, least-privilege accounts, patching, network segmentation, monitoring and backups together.

## Questions to test myself

1. Can I explain the difference between a threat and a vulnerability using one example?
2. Why doesn't HTTPS fix a broken access-control check?
3. Give one preventive control and one detective control.
4. What would least privilege look like for a normal application user?

## References

- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)
- [CISA Secure Our World](https://www.cisa.gov/secure-our-world)
