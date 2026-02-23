# 📋 REQUERIMIENTOS - Carrillo Abogados Legal Tech Platform

**Versión**: 1.0  
**Fecha**: 19 de Diciembre, 2025  
**Estado**: ✅ Documento Base Aprobado

---

## 📑 ÍNDICE

1. [Requerimientos Funcionales del Portal Público](#requerimientos-funcionales-del-portal-público)
2. [Requerimientos Funcionales del Sistema Interno](#requerimientos-funcionales-del-sistema-interno)
3. [Requerimientos Funcionales por Microservicio](#requerimientos-funcionales-por-microservicio)
4. [Requerimientos No Funcionales](#requerimientos-no-funcionales)
5. [Priorización MoSCoW](#priorización-moscow)

---

## 🌐 REQUERIMIENTOS FUNCIONALES DEL PORTAL PÚBLICO

### RF-PUB: Sitio Web Público

Estos requerimientos definen las funcionalidades visibles para visitantes anónimos del sitio web.

| ID | Requerimiento | Descripción | Prioridad |
|----|---------------|-------------|-----------|
| **RF-PUB-001** | Página de Inicio | Landing page con propuesta de valor, servicios destacados, CTA de contacto | MUST |
| **RF-PUB-002** | Quiénes Somos | Historia del bufete, misión, visión, valores | MUST |
| **RF-PUB-003** | Servicios | Listado general de servicios jurídicos ofrecidos | MUST |
| **RF-PUB-004** | Áreas de Práctica | 5 páginas detalladas por cada área de especialización | MUST |
| **RF-PUB-005** | Equipo | Perfiles de los 7 abogados con foto, biografía y especialidad | MUST |
| **RF-PUB-006** | Casos de Éxito | Testimonios y casos representativos (anonimizados) | SHOULD |
| **RF-PUB-007** | Blog | Artículos de actualidad legal, optimizados para SEO | SHOULD |
| **RF-PUB-008** | Preguntas Frecuentes | FAQ por área de práctica | SHOULD |
| **RF-PUB-009** | Contacto | Página con formulario, mapa, datos de contacto | MUST |
| **RF-PUB-010** | Formulario de Contacto | Captura de leads con validación y notificación automática | MUST |

### RF-INT: Funcionalidades Interactivas (Visitantes)

| ID | Requerimiento | Descripción | Prioridad |
|----|---------------|-------------|-----------|
| **RF-INT-001** | Agendar Cita Online | Sistema de booking para consultas iniciales | MUST |
| **RF-INT-002** | Chat en Vivo | Atención en tiempo real vía chat | SHOULD |
| **RF-INT-003** | Suscripción Newsletter | Captura de emails para marketing | COULD |
| **RF-INT-004** | Calculadoras Legales | Herramientas de cálculo (honorarios, términos) | COULD |
| **RF-INT-005** | Acceso Área Privada | Login para clientes existentes | MUST |
| **RF-INT-006** | Registro de Clientes | Auto-registro de nuevos clientes potenciales | SHOULD |

---

## 🔐 REQUERIMIENTOS FUNCIONALES DEL SISTEMA INTERNO

### RF-CLI: Gestión de Clientes

| ID | Requerimiento | Descripción | Prioridad |
|----|---------------|-------------|-----------|
| **RF-CLI-001** | Registro de Cliente | Crear cliente con datos completos (persona natural/jurídica) | MUST |
| **RF-CLI-002** | Edición de Cliente | Actualizar información de cliente existente | MUST |
| **RF-CLI-003** | Consulta de Cliente | Buscar cliente por nombre, NIT, cédula, email | MUST |
| **RF-CLI-004** | Historial de Cliente | Ver todos los casos asociados a un cliente | MUST |
| **RF-CLI-005** | Portal Cliente | Vista de cliente para consultar sus propios casos | MUST |
| **RF-CLI-006** | Comunicación Cliente | Mensajería interna cliente-abogado | SHOULD |
| **RF-CLI-007** | Notificaciones Cliente | Alertas de actualizaciones de caso | MUST |
| **RF-CLI-008** | Documentos Cliente | Upload/download de documentos por cliente | MUST |

### RF-CAS: Gestión de Casos Legales

| ID | Requerimiento | Descripción | Prioridad |
|----|---------------|-------------|-----------|
| **RF-CAS-001** | Crear Caso | Registro de nuevo caso legal vinculado a cliente | MUST |
| **RF-CAS-002** | Clasificar Caso | Asignar área de práctica, tipo de proceso, materia | MUST |
| **RF-CAS-003** | Asignar Abogado | Vincular abogado responsable y colaboradores | MUST |
| **RF-CAS-004** | Estados del Caso | Workflow: Nuevo → En Curso → Suspendido → Cerrado | MUST |
| **RF-CAS-005** | Línea de Tiempo | Historial cronológico de actuaciones del caso | MUST |
| **RF-CAS-006** | Tareas del Caso | Asignar y dar seguimiento a tareas específicas | SHOULD |
| **RF-CAS-007** | Términos Legales | Registro y alerta de términos procesales | MUST |
| **RF-CAS-008** | Contraparte | Registro de parte contraria y sus representantes | SHOULD |
| **RF-CAS-009** | Autoridad | Registro de juzgado/entidad donde cursa el proceso | SHOULD |
| **RF-CAS-010** | Radicado | Número de radicado del proceso (si aplica) | SHOULD |

### RF-DOC: Gestión de Documentos

| ID | Requerimiento | Descripción | Prioridad |
|----|---------------|-------------|-----------|
| **RF-DOC-001** | Subir Documento | Upload de archivos PDF, Word, Excel, imágenes | MUST |
| **RF-DOC-002** | Clasificar Documento | Categorización por tipo, caso, cliente | MUST |
| **RF-DOC-003** | Versionar Documento | Control de versiones de documentos | SHOULD |
| **RF-DOC-004** | Buscar Documento | Búsqueda por nombre, fecha, tipo, caso | MUST |
| **RF-DOC-005** | Compartir Documento | Compartir con cliente vía portal | SHOULD |
| **RF-DOC-006** | Plantillas | Biblioteca de plantillas de documentos legales | COULD |
| **RF-DOC-007** | Firmar Documento | Integración con firma electrónica (futuro) | COULD |
| **RF-DOC-008** | Google Drive Sync | Sincronización con Drive corporativo | SHOULD |

### RF-CAL: Calendario y Audiencias

| ID | Requerimiento | Descripción | Prioridad |
|----|---------------|-------------|-----------|
| **RF-CAL-001** | Crear Evento | Registro de audiencias, reuniones, términos | MUST |
| **RF-CAL-002** | Google Calendar Sync | Sincronización bidireccional con Calendar | MUST |
| **RF-CAL-003** | Recordatorios | Alertas configurables antes del evento | MUST |
| **RF-CAL-004** | Vista Calendario | Vista mensual/semanal/diaria de eventos | MUST |
| **RF-CAL-005** | Disponibilidad | Mostrar disponibilidad de abogados | SHOULD |
| **RF-CAL-006** | Booking Online | Reserva de citas desde portal público | MUST |
| **RF-CAL-007** | Confirmación Cita | Email de confirmación automático | MUST |
| **RF-CAL-008** | Cancelación/Reprogramación | Gestión de cambios de citas | SHOULD |

### RF-PAY: Gestión de Pagos

| ID | Requerimiento | Descripción | Prioridad |
|----|---------------|-------------|-----------|
| **RF-PAY-001** | Registro de Pago | Crear orden de pago para trámites gubernamentales | MUST |
| **RF-PAY-002** | Tipos de Pago | Clasificar por concepto (tasa, arancel, registro) | MUST |
| **RF-PAY-003** | Estado de Pago | Workflow: Pendiente → En Proceso → Pagado → Verificado | MUST |
| **RF-PAY-004** | Comprobante | Subir comprobante de pago realizado | MUST |
| **RF-PAY-005** | Asociar a Caso | Vincular pago a caso legal específico | MUST |
| **RF-PAY-006** | Reportes | Informe de pagos por período, caso, cliente | SHOULD |
| **RF-PAY-007** | Pago Online | Pasarela de pagos (futuro) | COULD |

### RF-NOT: Notificaciones

| ID | Requerimiento | Descripción | Prioridad |
|----|---------------|-------------|-----------|
| **RF-NOT-001** | Email Transaccional | Envío de emails automáticos por eventos | MUST |
| **RF-NOT-002** | Templates Email | Plantillas de email configurables | MUST |
| **RF-NOT-003** | Notificaciones Push | Alertas en navegador/app (futuro) | COULD |
| **RF-NOT-004** | SMS | Envío de SMS para alertas críticas | SHOULD |
| **RF-NOT-005** | WhatsApp | Integración con WhatsApp Business (futuro) | COULD |
| **RF-NOT-006** | Preferencias | Usuario configura qué notificaciones recibir | SHOULD |
| **RF-NOT-007** | Log de Envíos | Historial de notificaciones enviadas | MUST |

### RF-N8N: Automatizaciones e Integración n8n

| ID | Requerimiento | Descripción | Prioridad |
|----|---------------|-------------|-----------|
| **RF-N8N-001** | Bridge NATS-Webhooks | Escuchar eventos NATS y reenviar a webhooks n8n | MUST |
| **RF-N8N-002** | Lead Capture | Emitir evento `lead.capturado` al recibir formulario | MUST |
| **RF-N8N-003** | Lead Scoring Callback | Recibir score calculado por n8n y actualizar en BD | MUST |
| **RF-N8N-004** | Hot Lead Alert | Notificar abogado cuando n8n detecta lead HOT (≥70 pts) | MUST |
| **RF-N8N-005** | Respuesta < 1 min | Garantizar tiempo de respuesta a leads < 60 segundos | MUST |
| **RF-N8N-006** | Calendly Integration | Emitir/recibir eventos de citas agendadas | SHOULD |
| **RF-N8N-007** | Email Tracking | Recibir eventos de apertura/click de Mailersend | SHOULD |
| **RF-N8N-008** | Cliente Inactivo | Detectar y notificar clientes sin actividad 30+ días | SHOULD |
| **RF-N8N-009** | Caso Cerrado | Emitir evento para trigger de follow-up satisfacción | SHOULD |
| **RF-N8N-010** | Firestore Sync | Sincronizar leads entre Firestore (n8n) y PostgreSQL | SHOULD |
| **RF-N8N-011** | Blog Publish | Recibir contenido aprobado de MW#3 y publicar | COULD |
| **RF-N8N-012** | Logs de Ejecución | Registrar todas las ejecuciones de workflows | SHOULD |

**Ver arquitectura completa:** [ESTRATEGIA_AUTOMATIZACION.md](./ESTRATEGIA_AUTOMATIZACION.md)

---

## 🔧 REQUERIMIENTOS FUNCIONALES POR MICROSERVICIO

### client-service (Puerto 8200)

| RF-ID | Implementa | Estado |
|-------|------------|--------|
| RF-CLI-001 | ✅ CRUD Clientes | 90% |
| RF-CLI-002 | ✅ Actualización clientes | 90% |
| RF-CLI-003 | ✅ Búsqueda clientes | 90% |
| RF-CLI-004 | ⏳ Historial casos | Pendiente |
| RF-CLI-005 | ⏳ Portal cliente | Pendiente |
| RF-CLI-006 | ⏳ Mensajería | Pendiente |
| RF-CLI-007 | ⏳ Integrar con notification-service | Pendiente |
| RF-CLI-008 | ⏳ Integrar con document-service | Pendiente |

### case-service (Puerto 8300)

| RF-ID | Implementa | Estado |
|-------|------------|--------|
| RF-CAS-001 | ✅ CRUD Casos | 95% |
| RF-CAS-002 | ✅ Clasificación por área | 95% |
| RF-CAS-003 | ✅ Asignación abogado | 95% |
| RF-CAS-004 | ✅ Estados del caso | 95% |
| RF-CAS-005 | ✅ CaseActivity (timeline) | 95% |
| RF-CAS-006 | ⏳ Tareas | Pendiente |
| RF-CAS-007 | ⏳ Términos legales | Pendiente |
| RF-CAS-008 | ✅ Contraparte | 95% |
| RF-CAS-009 | ⏳ Autoridad/Juzgado | Pendiente |
| RF-CAS-010 | ✅ Radicado | 95% |

### document-service (Puerto 8500)

| RF-ID | Implementa | Estado |
|-------|------------|--------|
| RF-DOC-001 | ⏳ Upload documentos | 5% |
| RF-DOC-002 | ⏳ Clasificación | 5% |
| RF-DOC-003 | ⏳ Versionamiento | Pendiente |
| RF-DOC-004 | ⏳ Búsqueda | Pendiente |
| RF-DOC-005 | ⏳ Compartir | Pendiente |
| RF-DOC-006 | ⏳ Plantillas | Pendiente |
| RF-DOC-007 | ⏳ Firma electrónica | Futuro |
| RF-DOC-008 | ⏳ Google Drive sync | Pendiente |

### calendar-service (Puerto 8600)

| RF-ID | Implementa | Estado |
|-------|------------|--------|
| RF-CAL-001 | ⏳ Crear evento | 5% |
| RF-CAL-002 | ⏳ Google Calendar API | 5% |
| RF-CAL-003 | ⏳ Recordatorios | Pendiente |
| RF-CAL-004 | ⏳ Vista calendario | Pendiente |
| RF-CAL-005 | ⏳ Disponibilidad | Pendiente |
| RF-CAL-006 | ⏳ Booking online | Pendiente |
| RF-CAL-007 | ⏳ Confirmación email | Pendiente |
| RF-CAL-008 | ⏳ Reprogramación | Pendiente |

### payment-service (Puerto 8400)

| RF-ID | Implementa | Estado |
|-------|------------|--------|
| RF-PAY-001 | ⏳ Crear orden pago | 5% |
| RF-PAY-002 | ⏳ Tipos de pago | 5% |
| RF-PAY-003 | ⏳ Estados pago | Pendiente |
| RF-PAY-004 | ⏳ Subir comprobante | Pendiente |
| RF-PAY-005 | ⏳ Vincular a caso | Pendiente |
| RF-PAY-006 | ⏳ Reportes | Pendiente |
| RF-PAY-007 | ⏳ Pasarela pagos | Futuro |

### notification-service (Puerto 8700)

| RF-ID | Implementa | Estado |
|-------|------------|--------|
| RF-NOT-001 | ⏳ Email transaccional | 5% |
| RF-NOT-002 | ⏳ Templates | 5% |
| RF-NOT-003 | ⏳ Push notifications | Futuro |
| RF-NOT-004 | ⏳ SMS | Pendiente |
| RF-NOT-005 | ⏳ WhatsApp | Futuro |
| RF-NOT-006 | ⏳ Preferencias | Pendiente |
| RF-NOT-007 | ⏳ Log envíos | Pendiente |

### n8n-integration-service (Puerto 8800)

| RF-ID | Implementa | Estado |
|-------|------------|--------|
| RF-N8N-001 | ⏳ Bridge NATS-Webhooks | 15% |
| RF-N8N-002 | ⏳ Lead Capture Event | 5% |
| RF-N8N-003 | ⏳ Lead Scoring Callback | Pendiente |
| RF-N8N-004 | ⏳ Hot Lead Alert | Pendiente |
| RF-N8N-005 | ⏳ Response < 1 min | Pendiente |
| RF-N8N-006 | ⏳ Calendly Integration | Pendiente |
| RF-N8N-007 | ⏳ Email Tracking | Pendiente |
| RF-N8N-008 | ⏳ Cliente Inactivo | Pendiente |
| RF-N8N-009 | ⏳ Caso Cerrado Event | Pendiente |
| RF-N8N-010 | ⏳ Firestore Sync | Pendiente |
| RF-N8N-011 | ⏳ Blog Publish | Futuro |
| RF-N8N-012 | ⏳ Logs Ejecución | 5% |

---

## ⚙️ REQUERIMIENTOS NO FUNCIONALES

### RNF-SEC: Seguridad

| ID | Requerimiento | Descripción | Prioridad |
|----|---------------|-------------|-----------|
| **RNF-SEC-001** | Autenticación OAuth2 | Login con Google Workspace (@carrilloabgd.com) | MUST |
| **RNF-SEC-002** | Autorización RBAC | Control de acceso basado en roles | MUST |
| **RNF-SEC-003** | HTTPS/TLS | Todas las comunicaciones cifradas | MUST |
| **RNF-SEC-004** | Protección de Datos | Cumplimiento Ley 1581 de 2012 (Habeas Data) | MUST |
| **RNF-SEC-005** | Auditoría | Log de todas las acciones de usuarios | MUST |
| **RNF-SEC-006** | Secreto Profesional | Datos de casos con acceso restringido | MUST |
| **RNF-SEC-007** | Backup | Respaldos automáticos diarios | MUST |
| **RNF-SEC-008** | Cifrado en Reposo | Datos sensibles cifrados en BD | SHOULD |

### RNF-PER: Rendimiento

| ID | Requerimiento | Descripción | Prioridad |
|----|---------------|-------------|-----------|
| **RNF-PER-001** | Tiempo de Respuesta | API < 500ms en operaciones normales | SHOULD |
| **RNF-PER-002** | Concurrencia | Soporte mínimo 50 usuarios simultáneos | SHOULD |
| **RNF-PER-003** | Disponibilidad | Uptime 99.5% (excluye mantenimiento) | SHOULD |
| **RNF-PER-004** | Carga de Archivos | Soporte archivos hasta 50MB | MUST |

### RNF-ESC: Escalabilidad

| ID | Requerimiento | Descripción | Prioridad |
|----|---------------|-------------|-----------|
| **RNF-ESC-001** | Horizontal Scaling | Microservicios escalables independientemente | SHOULD |
| **RNF-ESC-002** | Kubernetes Ready | Despliegue en GKE/Kubernetes | MUST |
| **RNF-ESC-003** | Stateless Services | Servicios sin estado para escalar | MUST |

### RNF-INT: Integraciones

| ID | Requerimiento | Descripción | Prioridad |
|----|---------------|-------------|-----------|
| **RNF-INT-001** | Google Workspace | Gmail, Calendar, Drive, Meet | MUST |
| **RNF-INT-002** | N8N Pro | Automatización de workflows | SHOULD |
| **RNF-INT-003** | NATS/Pub-Sub | Mensajería asíncrona entre servicios | MUST |
| **RNF-INT-004** | API REST | Endpoints RESTful documentados con OpenAPI | MUST |

### RNF-OBS: Observabilidad

| ID | Requerimiento | Descripción | Prioridad |
|----|---------------|-------------|-----------|
| **RNF-OBS-001** | Logging | Logs centralizados (Loki) | MUST |
| **RNF-OBS-002** | Métricas | Prometheus + Grafana dashboards | SHOULD |
| **RNF-OBS-003** | Tracing | Distributed tracing (Micrometer) | SHOULD |
| **RNF-OBS-004** | Health Checks | Endpoints /actuator/health | MUST |
| **RNF-OBS-005** | Alertas | Notificaciones ante incidentes | SHOULD |

### RNF-UX: Experiencia de Usuario

| ID | Requerimiento | Descripción | Prioridad |
|----|---------------|-------------|-----------|
| **RNF-UX-001** | Responsive Design | Adaptable a móvil, tablet, desktop | MUST |
| **RNF-UX-002** | Accesibilidad | WCAG 2.1 nivel AA | SHOULD |
| **RNF-UX-003** | Idioma | Español (Colombia) | MUST |
| **RNF-UX-004** | Estilo | Moderno, profesional, no informal | MUST |
| **RNF-UX-005** | Compatibilidad | Chrome, Firefox, Safari, Edge últimas 2 versiones | MUST |

### RNF-LEG: Cumplimiento Legal

| ID | Requerimiento | Descripción | Prioridad |
|----|---------------|-------------|-----------|
| **RNF-LEG-001** | Ley 1581/2012 | Protección de datos personales | MUST |
| **RNF-LEG-002** | Política Privacidad | Publicada y aceptada por usuarios | MUST |
| **RNF-LEG-003** | Términos y Condiciones | Publicados y aceptados | MUST |
| **RNF-LEG-004** | Cookies | Aviso y consentimiento | MUST |
| **RNF-LEG-005** | Secreto Profesional | Confidencialidad abogado-cliente | MUST |

---

## 🎯 PRIORIZACIÓN MoSCoW

### MUST HAVE (MVP - 27 Marzo 2026)

**Portal Público:**
- Página de inicio con servicios
- Quiénes somos, áreas de práctica
- Formulario de contacto funcional
- Sistema de booking de citas

**Sistema Interno:**
- Gestión de clientes (CRUD)
- Gestión de casos legales (CRUD)
- Integración Google Calendar
- Notificaciones por email
- Autenticación OAuth2

### SHOULD HAVE (Post-MVP Q2 2026)

- Blog con CMS
- Chat en vivo
- Gestión de documentos avanzada
- Portal de cliente (vista casos)
- SMS notificaciones
- Reportes y analytics

### COULD HAVE (Futuro)

- Calculadoras legales
- Firma electrónica
- WhatsApp Business
- App móvil nativa
- Pasarela de pagos

### WON'T HAVE (Fuera de alcance)

- Inteligencia artificial legal
- Comparecencia virtual integrada
- Marketplace de servicios legales
- Multiidioma

---

## 📊 MATRIZ DE TRAZABILIDAD

```
┌──────────────────────────────────────────────────────────────────┐
│                    MICROSERVICIO                                  │
├──────────────┬─────────────────────────────────────────────────┬─┤
│ Requerimiento│ client │ case │ doc │ cal │ pay │ not │ n8n │api│
├──────────────┼─────────────────────────────────────────────────┼─┤
│ RF-CLI-*     │   ●    │      │     │     │     │     │     │   │
│ RF-CAS-*     │        │  ●   │     │     │     │     │     │   │
│ RF-DOC-*     │        │      │  ●  │     │     │     │     │   │
│ RF-CAL-*     │        │      │     │  ●  │     │     │     │   │
│ RF-PAY-*     │        │      │     │     │  ●  │     │     │   │
│ RF-NOT-*     │        │      │     │     │     │  ●  │     │   │
│ RF-N8N-*     │        │      │     │     │     │     │  ●  │   │
│ RF-PUB-*     │        │      │     │     │     │     │     │ ● │
│ RF-INT-*     │   ○    │      │     │  ○  │     │     │     │ ● │
│ RNF-SEC-*    │   ●    │  ●   │  ●  │  ●  │  ●  │  ●  │  ●  │ ● │
└──────────────┴─────────────────────────────────────────────────┴─┘

● = Responsable principal
○ = Contribuye/Colabora
```

---

## 🔗 DOCUMENTOS RELACIONADOS

- [MODELO_NEGOCIO.md](./MODELO_NEGOCIO.md) - Contexto de negocio
- [ROLES_USUARIOS.md](./ROLES_USUARIOS.md) - Definición de roles y permisos
- [CASOS_USO.md](./CASOS_USO.md) - Casos de uso detallados
- [ARQUITECTURA_FUNCIONAL.md](./ARQUITECTURA_FUNCIONAL.md) - Mapeo arquitectónico

---

*Documento basado en el Brief de Requerimientos de Carrillo ABGD SAS*
