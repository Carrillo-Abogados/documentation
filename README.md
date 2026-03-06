# Carrillo Abogados - Documentacion Centralizada

Repositorio OFICIAL y fuente unica de verdad para la documentacion de la plataforma **Carrillo Abogados Legal Tech** - sistema de gestion legal empresarial para Carrillo ABGD SAS, Cali, Colombia.

---

## Estructura

| Directorio | Contenido |
|------------|-----------|
| `business/` | Modelo de negocio, requerimientos, casos de uso, roles de usuarios, MVP roadmap |
| `architecture/` | Arquitectura tecnica, ADRs (Architecture Decision Records) |
| `development/` | Guias de desarrollo, usuarios de prueba, gestion de versiones |
| `operations/` | Deployment, GCP Cloud Run, observabilidad, secretos, migracion |
| `security/` | Gestion de secretos, seguridad CI/CD |
| `project/` | Estado del proyecto, historial de migracion |

---

## Repositorios de la Organizacion

| Repo | Proposito | Responsable |
|------|-----------|-------------|
| [backend-services](https://github.com/Carrillo-Abogados/backend-services) | 8 microservicios Spring Boot | Claude Code (Opus 4.6) |
| [frontend](https://github.com/Carrillo-Abogados/frontend) | Aplicacion Next.js 16 + React | Claude Code |
| [platform](https://github.com/Carrillo-Abogados/platform) | Infraestructura, Docker Compose, Helm, monitoring | Claude Code |
| [documentation](https://github.com/Carrillo-Abogados/documentation) | Este repositorio - documentacion oficial | Claude Code |
| [automation](https://github.com/Carrillo-Abogados/automation) | Workflows n8n marketing | Juan Jose Gomez |
| [openclaw-agency](https://github.com/Carrillo-Abogados/openclaw-agency) | OpenClaw multi-agent framework + skills | Juan Jose Gomez |

---

## Orden de Lectura Recomendado

1. **business/MVP_ROADMAP.md** - Que estamos construyendo (5 pilares del MVP)
2. **business/ROLES_USUARIOS.md** - Quien va a usar el sistema (4 roles)
3. **business/REQUERIMIENTOS.md** - Que funcionalidades necesitamos (100+ RFs)
4. **business/CASOS_USO.md** - Como interactuan los usuarios (17 casos de uso)
5. **business/ARQUITECTURA_FUNCIONAL.md** - Como lo implementamos (8 microservicios)
6. **business/MODELO_NEGOCIO.md** - Contexto empresarial del bufete
7. **architecture/ARCHITECTURE.md** - Arquitectura tecnica del sistema
8. **operations/DEPLOYMENT.md** - Como desplegamos a produccion

---

## Stack Tecnologico

| Categoria | Tecnologia |
|-----------|------------|
| **Backend** | Java 21, Spring Boot 3.3, Spring Cloud 2023.0.6 |
| **Frontend** | Next.js 16, React 18, TypeScript 5, Tailwind CSS |
| **Base de Datos** | PostgreSQL 16 (schemas separados por servicio) |
| **Mensajeria** | NATS JetStream (dev/staging), Google Pub/Sub (prod) |
| **Contenedores** | Docker + Google Jib |
| **Orquestacion** | Cloud Run (prod) + Kind cluster (local) |
| **Observabilidad** | Grafana LGTM (Prometheus, Loki, Tempo, Mimir) |
| **CI/CD** | GitHub Actions + Google Artifact Registry |
| **Seguridad** | Snyk + Trivy |
| **IA Development** | Claude Code (Opus 4.6) |

---

## MVP

- **Fecha objetivo**: 10 de Abril, 2026
- **Cliente**: Carrillo ABGD SAS, Cali, Colombia
- **Equipo**: 7 abogados + 2 administrativos
- **Desarrollador**: Alexis (Claude Code como IA principal)
