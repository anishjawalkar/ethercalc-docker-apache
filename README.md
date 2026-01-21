# EtherCalc Deployment (Docker + Apache Reverse Proxy)

Minimal, production-style deployment of **EtherCalc** using Docker and Redis, exposed securely through an **Apache reverse proxy** with HTTPS and authentication.

This repository intentionally keeps the setup simple to reflect real-world usage patterns for lightweight collaborative tools.

---

## Overview

EtherCalc is deployed as a Docker container backed by Redis for persistence.  
The application is bound to localhost and exposed externally only via Apache.

Key goals:
- Secure public access
- Simple authentication
- Minimal operational complexity
- Clean separation between proxy and application

---

## Architecture

Internet
|
[ HTTPS : Apache ]
|
[ Reverse Proxy + Auth ]
|
[ Docker Host ]
├── EtherCalc (8000 → 8083)
└── Redis

yaml
Copy code

---

## Components

- **EtherCalc** – collaborative spreadsheet application
- **Redis** – persistent backend store
- **Docker / Docker Compose** – container orchestration
- **Apache** – reverse proxy, TLS termination, authentication
- **Certbot** – TLS certificates (Let’s Encrypt)

---

## Deployment Summary

1. Start Redis and EtherCalc using Docker Compose  
2. Bind EtherCalc to `127.0.0.1` on the host  
3. Configure Apache reverse proxy with WebSocket support  
4. Enable HTTPS using Certbot  
5. Apply Basic Authentication at the proxy layer  

---

## Authentication

Authentication is handled at the Apache layer using **Basic Auth**.

This approach is:
- Simple
- Secure over HTTPS
- Easy to maintain
- Appropriate for small teams and internal tools

---

## Intended Use

- DevOps practice
- Self-hosted internal tools
- Learning reverse proxy and container patterns

This repository does **not** aim to provide:
- Advanced IAM
- Multi-tenant isolation
- OAuth or SSO integration

---

## Notes

- Domains and credentials are placeholders
- Etherpad is intentionally maintained in a separate repository
- Configuration files are simplified for clarity

---

## License

MIT License
