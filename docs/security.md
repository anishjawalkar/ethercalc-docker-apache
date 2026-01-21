# Security Model

This document outlines the security controls applied in this EtherCalc deployment.

---

## Security Principles

- Minimize exposed services
- Enforce security at the proxy layer
- Keep application containers isolated
- Prefer simple, auditable mechanisms

---

## Network Isolation

- EtherCalc binds only to localhost
- Redis is not exposed outside Docker
- Apache is the only public-facing service

---

## TLS

- HTTPS enforced via Let’s Encrypt
- TLS terminated at Apache
- Certificates managed using Certbot

---

## Authentication

Authentication is implemented using Apache Basic Auth.

Example:
```apache
<Location />
    AuthType Basic
    AuthName "EtherCalc"
    AuthBasicProvider file
    AuthUserFile /etc/apache2/ethercalc-users
    Require valid-user
</Location>
```
Credential Handling
Credentials are not stored in this repository

Passwords are managed via Apache user files

HTTPS protects credentials in transit

Logging
Apache access logs record authentication events

SSL and application traffic are logged separately

Limitations
No rate limiting

No MFA or SSO

Suitable for internal or small-team usage
