# MIGRATION_STANDARD.md - Carrillo Abogados
## Estándar de Infraestructura y Migración para Agentes IA

Este documento define las reglas de oro que cada repositorio (Backend, Frontend, Automation) debe seguir para integrarse profesionalmente en la infraestructura de Google Cloud.

---

### 1. Autenticación y Entorno (WSL)
Para trabajar con GCP, cada agente IA debe asegurarse de que el entorno WSL tiene instaladas:
- **gcloud CLI**: Para gestión de recursos.
- **Terraform**: Para infraestructura local.
- **Docker**: Para construcción de imágenes.

**Autenticación**: Los agentes deben usar `gcloud auth login` y `gcloud auth application-default login` para interactuar con la nube.

### 2. Estándar Docker (Containerization)
Cada microservicio DEBE incluir un `Dockerfile` multietapa (multi-stage) para optimizar el tamaño.
- **Puerto**: Todos los servicios deben escuchar en el puerto `8080`.
- **Registro**: Las imágenes deben subirse al Artifact Registry central:
  `us-central1-docker.pkg.dev/carrillo-admin-ops/carrillo-platform/{nombre-servicio}`

### 3. Jerarquía de Entornos (GCP Projects)
Cada agente desplegará sus servicios según el entorno:
- **Desarrollo**: `carrillo-dev-4811`
- **Staging**: `carrillo-staging-4811`
- **Producción**: `carrillo-prod-4811`

### 4. Variables de Entorno (Secrets)
**LEY DE SEGURIDAD**: Nunca subir archivos `.env` o secretos al repositorio.
- Usar **Google Cloud Secret Manager** para credenciales de base de datos, API keys y tokens.
- Los agentes IA deben automatizar la creación de estos secretos vía Terraform en sus propios repositorios.

### 5. Proceso de Entrega (Workflow)
1. **Plan**: Definir los recursos necesarios (Cloud Run, Cloud SQL, etc.) en Terraform.
2. **Build**: Construir la imagen Docker y subirla al registry de Ops.
3. **Deploy**: Aplicar los cambios en el proyecto de GCP correspondiente.

---
**Firmado**: Claude Code (Opus 4.6)
**Fecha**: 4 de Marzo de 2026
