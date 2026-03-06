# 🔐 Guía de Seguridad - CI/CD Pipeline

**Última Actualización**: 6 de Marzo, 2026
**Estado**: ✅ Integrado con GitHub Actions

---

## 📋 Herramientas de Seguridad

| Herramienta | Propósito | Integración | Estado |
|-------------|-----------|-------------|--------|
| **Snyk** | Vulnerabilidades en dependencias Maven | GitHub Actions (workflow summary) | ✅ Activo |
| **Trivy** | Escaneo de filesystem y dependencias | GitHub Actions (workflow summary) | ✅ Activo |
| **SonarCloud** | Análisis estático de código, code smells | NO configurado | ⏸️ Pospuesto |
| **OWASP ZAP** | DAST / Penetration testing | Manual / Workflow dispatch | ⏸️ Pospuesto |

> **Nota**: Los resultados de Snyk y Trivy se reportan en el **workflow summary** de GitHub Actions, no en GitHub Advanced Security (GHAS). No se usan SARIF uploads.

---

## 🛡️ Snyk

### Dashboard
- **URL**: https://app.snyk.io/org/alexisj16
- **Proyectos**: Todos los pom.xml de microservicios importados

### Configuración en GitHub Actions

El workflow `security-scan.yml` ejecuta:
1. **Snyk Open Source**: Escanea dependencias Maven

> **Nota**: `SNYK_TOKEN` está configurado como secret en el repo `backend-services`. Los resultados se publican en el workflow summary de GitHub Actions.

### Secrets Requeridos

```
SNYK_TOKEN: Tu token de API de Snyk
```

Para obtenerlo:
1. Ir a https://app.snyk.io/account
2. Copiar "Auth Token"
3. Agregar en GitHub → Settings → Secrets → Actions → New secret

### Interpretar Resultados

| Severidad | Acción Requerida |
|-----------|------------------|
| **Critical** | Corregir inmediatamente |
| **High** | Corregir antes del próximo release |
| **Medium** | Planificar corrección |
| **Low** | Evaluar si aplica |

---

## 📊 SonarCloud (POSPUESTO)

> **Estado**: NO configurado actualmente. Pospuesto para una fase posterior.

Cuando se configure, se necesitará:
- `SONAR_TOKEN` como GitHub secret
- URL: https://sonarcloud.io/account/security para generar token

---

## 🐳 Trivy

### Escaneo Automático

Trivy escanea:
1. **Filesystem**: Vulnerabilidades en código y configs
2. **Containers**: Imágenes Docker antes del push
3. **IaC**: Terraform, Kubernetes manifests

### Resultados

Los resultados se publican automáticamente en:
- GitHub Actions → Workflow summary (no GHAS/SARIF)

### Severidades Reportadas

Solo se reportan **HIGH** y **CRITICAL** para evitar ruido.

---

## 🕷️ OWASP ZAP (Opcional)

### Uso Manual

OWASP ZAP está configurado pero deshabilitado por defecto. Para ejecutar:

1. Ir a GitHub → Actions → Security Scan
2. Click "Run workflow"
3. Seleccionar rama y ejecutar

### Requisitos

- Tener un ambiente de staging accesible públicamente
- Configurar la URL target en el workflow

---

## 📋 Workflow de Seguridad

```
┌─────────────────────────────────────────────────────────────────┐
│                    SECURITY SCAN PIPELINE                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Trigger: Push to main/staging, Weekly schedule, Manual        │
│                                                                 │
│  ┌─────────────┐                    ┌─────────────┐            │
│  │   Snyk      │                    │   Trivy     │            │
│  │  Scan       │                    │   Scan      │            │
│  └──────┬──────┘                    └──────┬──────┘            │
│         │                                  │                    │
│         └──────────────┬───────────────────┘                    │
│                        │                                        │
│                        ▼                                        │
│                ┌──────────────┐                                │
│                │  Workflow    │                                │
│                │  Summary     │                                │
│                └──────────────┘                                │
│                                                                 │
│  Results:                                                       │
│  • GitHub Actions → Workflow Summary (reportes)                │
│  • Snyk Dashboard (https://app.snyk.io)                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## ⚙️ Configuración Inicial

### 1. Agregar Secrets en GitHub

```bash
# Ir a: GitHub → Settings → Secrets and variables → Actions

SNYK_TOKEN=<tu-token-snyk>
# SONAR_TOKEN - NO configurado actualmente (pospuesto)
```

### 2. Verificar Integración

1. Hacer push a main o staging
2. Ir a Actions → ver ejecución de "Security Scan"
3. Verificar resultados en cada dashboard

### 3. Configurar Notificaciones

En Snyk:
1. Settings → Notifications → Activar alertas por email

En SonarCloud:
1. Administration → Notifications → Configurar preferencias

---

## 📊 Estado Actual del Proyecto

### Snyk (según captura)

| Servicio | Critical | High | Medium | Low |
|----------|:--------:|:----:|:------:|:---:|
| api-gateway | 1 | 9 | 4 | 2 |
| n8n-integration-service | 0 | 12 | 5 | 2 |
| notification-service | 0 | 8 | 4 | 1 |
| calendar-service | 0 | 8 | 4 | 1 |
| case-service | 0 | 8 | 4 | 1 |
| document-service | 0 | 8 | 4 | 1 |
| payment-service | 0 | 8 | 4 | 1 |
| client-service | 0 | 8 | 4 | 1 |
| **TOTAL** | **1** | **80** | **83** | **62** |

### SonarCloud

> NO configurado actualmente. Pospuesto para una fase posterior.

### Próximos Pasos

1. Resolver el issue **Critical** en api-gateway (Snyk)
2. Agregar tests para mejorar coverage
3. Evaluar configuración de SonarCloud cuando sea prioritario

---

## 🔗 Enlaces Rápidos

- [Snyk Dashboard](https://app.snyk.io/org/alexisj16)
- [GitHub Actions - Security Scan](https://github.com/Carrillo-Abogados/backend-services/actions)
- [Security Scan Workflow](https://github.com/Carrillo-Abogados/backend-services/blob/dev/.github/workflows/security-scan.yml)

---

*Documentación de Seguridad CI/CD - Carrillo Abogados Legal Tech Platform*
