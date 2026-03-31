# NetTools-VelesAI

Enterprise-grade, vendor-agnostic network device management platform with AI-powered assistance and a unified control plane.

---

## Table of contents.

- [Overview](#overview)
- [Architecture Overview](#architecture-overview)
- [Core Capabilities](#core-capabilities)
  - [Unified Control Plane (UCP)](#unified-control-plane-ucp)
  - [Visual Network Canvas](#visual-network-canvas)
  - [VelesAI – AI Assistant](#velesai--ai-assistant)
  - [Vulnerabilities & Compliance](#vulnerabilities--compliance)
  - [Financial & Lifecycle Controls](#financial--lifecycle-controls)
  - [Device & Site Management](#device--site-management)
- [Technology Stack](#technology-stack)
  - [Backend](#backend)
  - [Frontend](#frontend)
  - [Infrastructure](#infrastructure)
- [Security Architecture](#security-architecture)
- [Observability](#observability)
- [Roadmap](#roadmap-high-level)
- [Project Status](#project-status)
- [License](#license)

---

## Overview

NetTools-VelesAI is an enterprise-grade, vendor-agnostic network management platform designed to replace text-heavy, CLI-driven workflows with a visual, AI-augmented operational model.

The platform unifies topology, configuration state, security posture, and financial impact into a single operational view so engineers and decision-makers can see the network rather than parsing text configurations.

NetTools-VelesAI combines:

- a Unified Control Plane for managing multi-vendor network devices
- **automatic tunnel creation** for secure connectivity to agents and remote devices without manual VPN or port-forward setup
- a visual network canvas for topology, dependency, and change-impact analysis
- AI-assisted reasoning for configuration, validation, and troubleshooting
- **upgrade with AI inline**—context, checks, and guidance in the same flow as firmware and lifecycle changes
- **firmware and software upgrades** with scheduling, rollout planning, and vendor-aligned target versions
- **configuration backups**—automated capture, retention, and restore-oriented exports before and after material changes
- vulnerability and lifecycle awareness (CVEs, firmware versions, end-of-life status)
- **compliance and security frameworks**—structured views that map posture and controls to common enterprise frameworks for audits and gap analysis
- financial and operational context (CSV-based cost, inventory, and compliance data)

The visual canvas is the primary interaction surface, linking devices, policies, VPNs, vulnerabilities, and costs into a coherent, continuously updated model. AI augments this model by providing context-aware explanations, risk assessment, and guided actions, while keeping humans firmly in control of every operational decision.

NetTools-VelesAI is built for complex, multi-site, multi-vendor environments where reliability, clarity, security, and operational cost control are critical.

---

## Architecture Overview

NetTools-VelesAI follows a modern, layered architecture with a clear separation of concerns.

Presentation layer

- Web UI (React 19)
- API clients (REST / WebSocket)

Application layer

- Frontend (Vite + React)
- Backend (FastAPI)
- WebSocket server

Business logic layer

- Unified Control Plane
- Policy & config services
- Upgrade and backup orchestration
- AI tool orchestration

Data layer

- PostgreSQL
- pgvector (RAG embeddings)
- Encrypted credential storage

Integration layer

- VyOS agents (WebSocket)
- Cisco devices (SSH)
- Ollama (local LLM)
- External APIs
- **Automatic tunnel creation** for agent and operator paths (orchestrated secure tunnels without ad-hoc manual setup)

---

## Core Capabilities

### Unified Control Plane (UCP)

A next-generation control plane for enterprise and industrial networks.

Key features:

- Multi-vendor device support (VyOS, Cisco IOS / IOS-XE, Juniper, OPNsense)
- Configuration lifecycle: draft → pending → applied → confirmed
- Commit-confirm pattern with automatic rollback
- Firewall, VPN, and service policy management
- Configuration drift detection
- Batch command execution and deployment optimization
- Real-time monitoring and health checks
- **Firmware and software upgrades**: plan targets, stage rollouts, track progress, and align with lifecycle policy
- **Configuration backups**: scheduled snapshots, retention, and pre-change checkpoints tied to the configuration lifecycle
- **Automatic tunnel creation** where the control plane establishes required connectivity to agents and devices according to policy

![Unified Control Plane – Device Context](UCP.png)
![Unified Control Plane – Commit Confirm](CommitConfirm.png)


### Visual Network Canvas

At the core of NetTools-VelesAI is a visual network canvas that enables engineers to see the network instead of parsing raw configuration text.

The canvas provides:

- A live, interactive topology view across sites and vendors
- Visual representation of devices, links, zones, and dependencies
- Context-aware actions (inspect, configure, validate, deploy)
- Real-time status indicators (health, drift, VPN state)

The visual layer acts as a reasoning surface: changes, risks, and dependencies are visible before commands are executed.

![Visual Network Canvas – Device Context](VisualCanvas.png)
![Unified Control Plane – IPSec](IpSec.png)

### VelesAI – AI Assistant

An AI-powered assistant designed to support engineers, not replace them.

Capabilities:

- Retrieval-Augmented Generation (RAG) over device configurations
- Context-aware chat with persistent memory
- Tool-based reasoning (inventory, analysis, config, knowledge)
- Web search and vulnerability knowledge integration
- Streaming responses and file-assisted analysis
- **Upgrade with AI inline**: firmware and lifecycle flows stay in-context—VelesAI explains options, surfaces risks, suggests validation steps, and answers questions without leaving the upgrade experience

![Veles – Device Context](Veles.png)
![Veles – Upgrades](Upgrades.png)

### Vulnerabilities & Compliance

NetTools-VelesAI includes a dedicated vulnerability and lifecycle awareness layer.

Features:

- CVE ingestion and correlation (device, OS, firmware)
- Impact mapping: vulnerability → affected devices → sites
- End-of-life and end-of-support tracking
- Upgrade recommendations aligned with vendor guidance
- **Security & compliance frameworks**: map inventory, configuration, and vulnerability posture to recognized frameworks (e.g. NIST CSF, ISO 27001 family, CIS Controls) for consistent audit language and gap visibility—not a certification substitute, but a single place to reason about control coverage
- Compliance-ready views for audits and reporting

Vulnerabilities are treated as operational risk, not isolated alerts.

![Vulnerabilities View](Vuln.png)

![End-of-Life & Compliance View](Compliance.png)

![Security Frameworks Wiew](SecurityFrameworks.png)

### Financial & Lifecycle Controls

NetTools-VelesAI connects technical network state with financial and lifecycle awareness.

Capabilities:

- Device-level CapEx and OpEx tracking
- License and support contract visibility
- Firmware lifecycle awareness (recommended, non-standard, end-of-life)
- CSV import/export for finance, inventory, and audits
- Aggregated cost and risk views per site or region

This enables engineering, security, and finance teams to reason over the same source of truth.

![Finance – Finance context](Finnance.png)

### Device & Site Management

- Multi-vendor inventory and classification
- Site-based topology organization
- Firmware lifecycle and compliance tracking
- **Upgrades**: target-version planning, scheduling, batched or staged rollouts, and post-upgrade validation hooks
- Vulnerability correlation (CVE → device impact)
- **Backups**: automated configuration backups, retention policies, on-demand exports, and pre-change snapshots for safer rollbacks
- SSH / API-based data collection with vendor parsers
- **Automatic tunnel creation** to reach devices and agents where direct routing is not available
- **Inline AI** alongside upgrade and maintenance tasks for guided, auditable changes

![CSV Import & Export](CSV.png)

---

## Technology Stack

### Backend

- FastAPI — async web framework
- SQLModel / SQLAlchemy 2.0
- PostgreSQL 16+
- pgvector — semantic embeddings
- Ollama — local LLM inference
- Paramiko / Netmiko — device connectivity
- WebSockets — real-time agent communication
- Prometheus — metrics
- Sentry — error tracking

### Frontend

- React 19
- Vite
- Tailwind CSS
- Radix UI
- React Router
- Axios
- XTerm.js — interactive terminal
- Chart.js — visual analytics

### Infrastructure

- Docker & Docker Compose
- Nginx (production reverse proxy)
- GitHub Actions (CI/CD)

---

## Security Architecture

- Encrypted credential storage (AES-256)
- Role-based access control (RBAC)
- SSH key and certificate-based device authentication
- Mutual TLS for agent communication
- Full audit and communication logging
- Secure defaults across the stack

---

## Observability

- Structured JSON logging
- Correlation IDs for request tracing
- Prometheus metrics endpoint
- Health checks for database, agents, and external services
- Real-time device and VPN status monitoring

---

## Roadmap (High Level)

- Multi-region support
- Predictive analytics and AI-assisted remediation
- External REST API for third-party integrations
- Advanced authentication (OAuth2, SAML, MFA)

---

## Project Status

Actively developed — MVP+ with working UI, backend, and AI integration. Designed for pilot deployments with enterprise and industrial partners.

---

## License

License will be defined prior to first public release / pilot agreement.
