# Architecture Overview

This document describes the architecture of the EtherCalc deployment used in this repository.

---

## High-Level Design

The system follows a simple reverse-proxy architecture where Apache controls all external access.

Client
|
HTTPS
|
Apache (Auth + TLS)
|
Docker Host
├── EtherCalc
└── Redis

yaml
Copy code

---

## Design Choices

- Apache acts as the single entry point
- EtherCalc is not exposed publicly
- Redis is accessible only within Docker
- Authentication is handled before traffic reaches the application

---

## Port Strategy

| Service   | Internal | Host Binding |
|----------|----------|--------------|
| EtherCalc | 8000 | 127.0.0.1:8083 |
| Redis | 6379 | Docker internal |

---

## WebSockets

EtherCalc uses WebSockets for live collaboration.  
Apache proxies WebSocket traffic using `proxy_wstunnel`.

---

## Scope

This architecture prioritizes:
- Simplicity
- Security
- Ease of maintenance

It intentionally avoids advanced scaling or HA features.
