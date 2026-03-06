# CLAUDE.md - Documentation Repository

## Purpose
Repositorio OFICIAL y fuente unica de verdad de toda la documentacion del proyecto Carrillo Abogados Legal Tech.

## Organization Repositories

| Repo | Purpose | Responsible |
|------|---------|-------------|
| [backend-services](https://github.com/Carrillo-Abogados/backend-services) | 8 Spring Boot microservices (Java 21) | Claude Code |
| [frontend](https://github.com/Carrillo-Abogados/frontend) | Next.js 16 + React 18 application | Claude Code |
| [platform](https://github.com/Carrillo-Abogados/platform) | Infrastructure: Docker Compose, Helm, K8s, monitoring | Claude Code |
| **documentation** | **This repo** - all project documentation (OFFICIAL) | Claude Code |
| [automation](https://github.com/Carrillo-Abogados/automation) | n8n marketing automation workflows | Juan Jose Gomez |
| [openclaw-agency](https://github.com/Carrillo-Abogados/openclaw-agency) | OpenClaw multi-agent framework + skills | Juan Jose Gomez |

## Content Structure

- **business/** - Business model, requirements (100+ RFs), use cases, user roles, MVP roadmap
- **architecture/** - System architecture, ADR-005 (database), ADR-006 (K8s local)
- **development/** - Dev guides, test users, version stability, feature backlog
- **operations/** - Deployment, GCP Cloud Run, observability, secrets, migration standard
- **security/** - Secrets management policy, CI/CD security tools
- **project/** - Project status (PROYECTO_ESTADO), migration history

## Key Information

- **MVP Target**: 10 April 2026
- **Stack**: Java 21 + Spring Boot 3.3 + PostgreSQL 16 + NATS + Next.js 16
- **8 Microservices**: api-gateway (8080), client-service (8200), case-service (8300), payment-service (8400), document-service (8500), calendar-service (8600), notification-service (8700), n8n-integration-service (8800)
- **4 User Roles**: Visitor, Client, Lawyer, Administrator
- **Infrastructure**: GCP (Cloud Run + Cloud SQL), Docker, Terraform
- **CI/CD**: GitHub Actions + Google Artifact Registry
- **Security**: Snyk + Trivy

## Guidelines

- This repo is the **single source of truth** for business requirements and project documentation
- Reference this repo when you need context about what we're building and why
- Spanish for documentation content, English for code examples
- Do not duplicate documentation that already exists here into other repos
- When modifying docs, maintain relative links within the same directory
- Claude Code is the sole AI developer — no Copilot, no Gemini for development
