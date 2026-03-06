# 🔄 ESTRATEGIA DE AUTOMATIZACIÓN - Integración Plataforma + n8n

**Versión**: 2.0
**Fecha**: 21 de Enero, 2026
**Estado**: ✅ Integrado con carpeta /automation/ (fuente de verdad)

> ⚠️ **NOTA IMPORTANTE**: La documentación técnica detallada de workflows n8n se encuentra en `/automation/`. Este documento proporciona el contexto de negocio de la integración.

---

## 📋 RESUMEN EJECUTIVO

Este documento define la **integración entre la plataforma web (microservicios Spring Boot)** y el **sistema de automatización de marketing (n8n)** para Carrillo Abogados.

### Modelo Estratégico: Flywheel + Inbound

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                     ECOSISTEMA CARRILLO ABOGADOS                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌───────────────────────────────────────────────────────────────────────┐ │
│  │                 PORTAL WEB (Microservicios Spring Boot)               │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  │ │
│  │  │  Captura    │  │  Gestión    │  │   Portal    │  │   Portal    │  │ │
│  │  │   Leads     │  │   Casos     │  │  Clientes   │  │   Blog      │  │ │
│  │  │ (Formulario)│  │  (Abogados) │  │  (Clientes) │  │   (SEO)     │  │ │
│  │  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘  │ │
│  └─────────┼────────────────┼────────────────┼────────────────┼─────────┘ │
│            │                │                │                │           │
│            ▼                ▼                ▼                ▼           │
│  ┌───────────────────────────────────────────────────────────────────────┐ │
│  │                    NATS (Event Bus)                                   │ │
│  │     lead.capturado | caso.creado | cliente.inactivo | blog.publicado │ │
│  └──────────────────────────────┬────────────────────────────────────────┘ │
│                                 │                                          │
│                                 ▼                                          │
│  ┌───────────────────────────────────────────────────────────────────────┐ │
│  │                n8n-integration-service (Puerto 8800)                  │ │
│  │                    Bridge Bidireccional                               │ │
│  └──────────────────────────────┬────────────────────────────────────────┘ │
│                                 │                                          │
│                                 ▼                                          │
│  ┌───────────────────────────────────────────────────────────────────────┐ │
│  │                    n8n Cloud (Automatizaciones)                       │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐                │ │
│  │  │ MW#1 CAPTURA │  │ MW#2 RETENCIÓN│ │ MW#3 SEO     │                │ │
│  │  │ 7 workflows  │  │ 5 workflows  │  │ 5 workflows  │                │ │
│  │  │ 108 nodos    │  │ 72 nodos     │  │ 60 nodos     │                │ │
│  │  └──────────────┘  └──────────────┘  └──────────────┘                │ │
│  └───────────────────────────────────────────────────────────────────────┘ │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 🎯 OBJETIVOS DE NEGOCIO

### KPIs del Sistema Integrado

| Métrica | Actual (Manual) | Objetivo (Automatizado) | Impacto |
|---------|----------------:|------------------------:|---------|
| Leads procesados/mes | 20 | 300+ | 15x crecimiento |
| Tiempo primera respuesta | 4-24 horas | < 1 minuto | 1440x más rápido |
| Tasa de conversión | ~5% | 15%+ | 3x mejora |
| Horas semanales gestión | 20+ | 5 | 4x menos tiempo |
| Clientes nuevos/año | ~15 | 100+ | $350M+ COP ingresos |

### Mercado Objetivo

| Criterio | Valor |
|----------|-------|
| **Segmento** | PyMEs tecnológicas en Colombia |
| **Tamaño mercado** | 1,678 empresas objetivo |
| **Ticket promedio** | $3.5M - $7M COP |
| **Diferenciador** | Dr. Omar Carrillo - 15 años en SIC |

---

## 🔌 LOS 3 MEGA-WORKFLOWS DE AUTOMATIZACIÓN

### Arquitectura Hub & Spoke

Cada MEGA-WORKFLOW sigue un patrón de orquestador (Hub) y sub-workflows especializados (Spokes):

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                          3 MEGA-WORKFLOWS                                    │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   MW#1: CAPTURA          MW#2: RETENCIÓN        MW#3: SEO CONTENT           │
│   Lead → Cliente         Cliente → Recompra     Tráfico → Lead              │
│                                                                              │
│   ┌────────────────┐    ┌────────────────┐     ┌────────────────┐           │
│   │ A: Orquestador │    │ B: Orquestador │     │ C: Orquestador │           │
│   │ Lead Lifecycle │    │ Client Relat.  │     │ Content Factory│           │
│   └───────┬────────┘    └───────┬────────┘     └───────┬────────┘           │
│           │                     │                      │                     │
│   ┌───────┴───────┐     ┌───────┴───────┐      ┌───────┴───────┐            │
│   │ SUB-A: Intake │     │ SUB-G: Segment│      │ SUB-K: Keywords│           │
│   │ SUB-B: Hot Not│     │ SUB-H: News   │      │ SUB-L: Writer  │           │
│   │ SUB-C: Response│    │ SUB-I: React. │      │ SUB-M: Publish │           │
│   │ SUB-D: Nurture│     │ SUB-J: Upsell │      │ SUB-N: Tracker │           │
│   │ SUB-E: Track  │     └───────────────┘      └────────────────┘           │
│   │ SUB-F: Meeting│                                                          │
│   └───────────────┘                                                          │
│                                                                              │
│   TOTAL: 17 workflows, 240 nodos                                            │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## 🔗 INTEGRACIÓN PLATAFORMA WEB ↔ n8n

### Puntos de Integración

| Origen | Evento | Destino n8n | Acción |
|--------|--------|-------------|--------|
| **Portal Público** | Formulario contacto enviado | MW#1 → SUB-A | Captura, scoring, respuesta IA |
| **Portal Público** | Cita agendada (Calendly) | MW#1 → SUB-F | Sincronizar, notificar |
| **client-service** | Cliente registrado | MW#2 → SUB-G | Segmentación inicial |
| **case-service** | Caso cerrado | MW#2 → SUB-I | Programar seguimiento |
| **Blog (CMS)** | Artículo publicado | MW#3 → SUB-N | Tracking SEO |
| **notification-service** | Email abierto/click | MW#1 → SUB-E | Actualizar engagement |

### Webhooks Requeridos en n8n

| Webhook | URL | Método | Payload |
|---------|-----|--------|---------|
| Lead Events | `/lead-events` | POST | `{ event_type, payload }` |
| Email Events | `/email-events` | POST | Mailersend webhook |
| Meeting Events | `/meeting-events` | POST | Calendly webhook |
| Blog Events | `/blog-events` | POST | WordPress webhook |

### Credenciales Configuradas

| Servicio | Estado | Uso |
|----------|--------|-----|
| Gmail OAuth2 | ✅ Activo | Envío emails, respuestas |
| Firestore | ✅ Activo | Almacenamiento leads |
| Google Gemini | ✅ Activo | Generación contenido IA |
| Mailersend | ⚪ Pendiente | Email marketing (MW#2) |
| WordPress REST | ⚪ Pendiente | Publicación blog (MW#3) |
| Google Search Console | ⚪ Pendiente | Tracking SEO (MW#3) |

---

## 📤 EVENTOS QUE EMITE LA PLATAFORMA

### Desde client-service

| Evento NATS | Trigger | Datos | Acción n8n |
|-------------|---------|-------|------------|
| `lead.capturado` | Formulario web | nombre, email, empresa, servicio, mensaje | MW#1: Scoring + Respuesta IA |
| `cliente.creado` | Registro cliente | clientId, tipo, email | MW#2: Segmentación inicial |
| `cliente.inactivo` | 30 días sin interacción | clientId, ultimaActividad | MW#2: Reactivación |

### Desde case-service

| Evento NATS | Trigger | Datos | Acción n8n |
|-------------|---------|-------|------------|
| `caso.cerrado` | Estado → CLOSED | caseId, clientId, tipoServicio | MW#2: Follow-up satisfacción |
| `caso.ganado` | Marcado como exitoso | caseId, area, resultado | MW#2: Solicitar testimonio |

### Desde calendar-service

| Evento NATS | Trigger | Datos | Acción n8n |
|-------------|---------|-------|------------|
| `cita.agendada` | Nueva cita booking | eventId, clientEmail, fecha | MW#1: Confirmación + prep |
| `cita.cancelada` | Cancelación | eventId, motivo | MW#1: Re-agendar automático |

---

## 📥 EVENTOS QUE RECIBE LA PLATAFORMA

### n8n → n8n-integration-service

| Webhook | Origen | Datos | Acción Plataforma |
|---------|--------|-------|-------------------|
| `/lead-scored` | SUB-A | leadId, score, category | Crear/actualizar en client-service |
| `/lead-hot` | SUB-B | leadId, urgency | Notificar abogado asignado |
| `/upsell-detected` | SUB-J | clientId, opportunity | Crear tarea en case-service |
| `/content-ready` | SUB-L | articleId, content | Publicar en blog (document-service) |

---

## 🎯 MW#1: CAPTURA Y CONVERSIÓN (Detalle)

### Flujo Completo: Lead desde Formulario Web

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                    FLUJO: CAPTURA DE LEAD                                    │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  PORTAL WEB                                                                  │
│  ┌─────────────────┐                                                        │
│  │ Formulario      │                                                        │
│  │ Contacto        │                                                        │
│  └────────┬────────┘                                                        │
│           │                                                                  │
│           ▼                                                                  │
│  ┌─────────────────┐     ┌─────────────────┐                               │
│  │ client-service  │────►│ NATS            │                               │
│  │ POST /leads     │     │ lead.capturado  │                               │
│  └─────────────────┘     └────────┬────────┘                               │
│                                   │                                          │
│  n8n-integration-service          │                                          │
│  ┌─────────────────┐              │                                          │
│  │ Escucha NATS    │◄─────────────┘                                          │
│  │ Envía a n8n     │                                                        │
│  └────────┬────────┘                                                        │
│           │                                                                  │
│           ▼                                                                  │
│  n8n Cloud                                                                   │
│  ┌─────────────────┐                                                        │
│  │ MW#1 Orquestador│                                                        │
│  │ /lead-events    │                                                        │
│  └────────┬────────┘                                                        │
│           │                                                                  │
│           ▼                                                                  │
│  ┌─────────────────┐                                                        │
│  │ SUB-A: Intake   │                                                        │
│  │ • Validar       │                                                        │
│  │ • Scoring       │     SCORING                                            │
│  │ • Categorizar   │     Base: 30 pts                                       │
│  └────────┬────────┘     Servicio "marca": +20 pts                          │
│           │              Mensaje > 50 chars: +10 pts                         │
│           │              Tiene teléfono: +10 pts                             │
│           │              Tiene empresa: +10 pts                              │
│           │              Email corporativo: +10 pts                          │
│           │              Cargo C-Level: +20 pts                              │
│           │                                                                  │
│           ▼                                                                  │
│  ┌─────────────────┐                                                        │
│  │ Categoría?      │                                                        │
│  ├─────────────────┤                                                        │
│  │ HOT (≥70)  ────►│──► SUB-B: Notificar Dr. Carrillo inmediatamente       │
│  │ WARM (40-69) ──►│──► SUB-C: Respuesta IA + Nurturing                    │
│  │ COLD (<40)  ───►│──► Respuesta genérica + Nurturing básico              │
│  └─────────────────┘                                                        │
│           │                                                                  │
│           ▼                                                                  │
│  ┌─────────────────┐                                                        │
│  │ SUB-C: Response │                                                        │
│  │ (Google Gemini) │     < 60 segundos desde captura                        │
│  │ Email IA        │                                                        │
│  └────────┬────────┘                                                        │
│           │                                                                  │
│           ▼                                                                  │
│  LEAD RECIBE EMAIL PERSONALIZADO EN < 1 MINUTO                              │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

### Secuencia de Nurturing (12 emails)

| # | Día | Objetivo | Contenido |
|---|-----|----------|-----------|
| 1 | 0 | Bienvenida | Presentación firma + Valor |
| 2 | 3 | Educativo | ¿Por qué proteger tu marca? |
| 3 | 7 | Case Study | Historia de éxito cliente |
| 4 | 10 | Valor agregado | Checklist PI gratuito |
| 5 | 14 | Urgencia | Riesgos de no proteger |
| 6 | 21 | Testimonial | Video Dr. Carrillo |
| 7 | 28 | Oferta | Consulta inicial gratuita |
| 8 | 35 | Re-engagement | ¿Sigues interesado? |
| 9 | 42 | Educativo | Tendencias PI 2026 |
| 10 | 49 | Last chance | Última oportunidad |
| 11 | 56 | Break-up | Email de despedida |
| 12 | 90 | Win-back | Re-activación |

---

## 🔄 MW#2: RETENCIÓN (Estrategia Flywheel)

### Segmentación por Comportamiento

| Segmento | Criterio | Frecuencia Contacto | Contenido |
|----------|----------|---------------------|-----------|
| **ENGAGED** 🟢 | Opens > 3, Clicks > 1 últimos 30d | Semanal | Newsletter premium |
| **AT-RISK** 🟡 | No opens últimos 15d | Cada 3 días | Re-engagement |
| **DORMANT** 🔴 | No actividad 30+ días | Secuencia 3 emails | Reactivación |
| **CHURNED** ⬛ | No responde a reactivación | Ninguno | Archivado |

### Ciclo de Ejecución

```
06:00 AM  →  SUB-G: Segmentación (actualiza campo "segment" en Firestore)
10:00 AM  →  SUB-H: Newsletter (envía a ENGAGED)
02:00 PM  →  SUB-I: Reactivación (contacta DORMANT)
On-demand →  SUB-J: Upsell (detecta oportunidades)
```

---

## 📊 MW#3: FÁBRICA DE CONTENIDO SEO

### Ciclo de Producción

| Fase | Frecuencia | Workflow | Output |
|------|------------|----------|--------|
| Investigación | 1x/mes | SUB-K | 20-30 keywords priorizadas |
| Escritura | 1x/semana | SUB-L | Borrador 2000+ palabras |
| Revisión | Asíncrona | HUMANO | Aprobado/Rechazado |
| Publicación | On-demand | SUB-M | Artículo en blog |
| Monitoreo | Diario | SUB-N | Métricas ranking |

### Criterios de Keywords

| Criterio | Valor |
|----------|-------|
| Volumen mínimo | > 100 búsquedas/mes |
| Dificultad máxima | KD < 30 |
| Tipo | Long-tail (3-5 palabras) |
| Intención | Informacional o transaccional |

---

## 🛠️ IMPACTO EN MICROSERVICIOS

### Cambios Requeridos

| Microservicio | Cambio | Prioridad |
|---------------|--------|-----------|
| **client-service** | Endpoint POST /leads para captura formulario | CRÍTICO |
| **client-service** | Emitir evento `lead.capturado` a NATS | CRÍTICO |
| **client-service** | Campo `leadScore`, `leadCategory` en entidad | ALTO |
| **n8n-integration-service** | Implementar bridge NATS ↔ n8n webhooks | CRÍTICO |
| **n8n-integration-service** | Endpoints para recibir callbacks de n8n | ALTO |
| **notification-service** | Integrar con Mailersend para tracking | MEDIO |
| **calendar-service** | Integrar con Calendly para booking | ALTO |
| **document-service** | API para publicación blog (CMS) | MEDIO |

### Modelo Lead en client-service

```java
@Entity
public class Lead {
    @Id
    private UUID id;

    private String nombre;
    private String email;
    private String telefono;
    private String empresa;
    private String cargo;
    private String servicio; // Área de práctica de interés
    private String mensaje;

    // Scoring (calculado por n8n)
    private Integer leadScore;        // 0-100
    private LeadCategory category;    // HOT, WARM, COLD
    private LeadStatus status;        // NUEVO, NURTURING, CONVERTIDO, CHURNED

    // Tracking
    private Integer emailsSent;
    private Integer emailsOpened;
    private Integer emailsClicked;
    private LocalDateTime lastContact;
    private LocalDateTime lastEngagement;

    // Conversión
    private UUID clientId;           // Si se convierte en cliente
    private LocalDateTime convertedAt;

    private LocalDateTime createdAt;
    private LocalDateTime updatedAt;
}
```

---

## 📅 ROADMAP DE INTEGRACIÓN

### Fase 1: Pre-Lanzamiento (Q4 2025 - Q1 2026)

| Semana | Entregable | Responsable |
|--------|------------|-------------|
| S1-2 | Endpoint /leads en client-service | Backend |
| S3-4 | n8n-integration-service bridge NATS | Backend |
| S5-6 | MW#1 SUB-A, SUB-B, SUB-C completos | Marketing |
| S7-8 | Integración E2E formulario → n8n → respuesta | Ambos |

### Fase 2: Lanzamiento (Marzo 2026)

| Semana | Entregable | Responsable |
|--------|------------|-------------|
| S1-2 | MW#1 completo (7 workflows) | Marketing |
| S3-4 | Integración Calendly + calendar-service | Backend |
| S5-6 | Testing E2E con leads reales | Ambos |

### Fase 3: Post-Lanzamiento (Q2 2026)

| Semana | Entregable | Responsable |
|--------|------------|-------------|
| S1-4 | MW#2 Retención (5 workflows) | Marketing |
| S5-8 | MW#3 SEO Content (5 workflows) | Marketing |
| S9-12 | Blog CMS + document-service | Backend |

---

## 📚 DOCUMENTOS RELACIONADOS

> ⚠️ **FUENTE DE VERDAD**: Todos los documentos técnicos de n8n están en `/automation/`

| Documento | Ubicación | Descripción |
|-----------|-----------|-------------|
| **Punto de Entrada** | [/automation/README.md](../../automation/README.md) | Inicio documentación automation |
| **Índice Completo** | [/automation/docs/00_INDEX.md](../../automation/docs/00_INDEX.md) | Navegación completa |
| **Arquitectura General** | [/automation/docs/technical/arquitectura/00_ARQUITECTURA_GENERAL.md](../../automation/docs/technical/arquitectura/00_ARQUITECTURA_GENERAL.md) | Visión completa 3 MEGA-WORKFLOWS |
| **MW#1 Captura** | [/automation/docs/technical/arquitectura/01_MEGA_WORKFLOW_1_CAPTURA.md](../../automation/docs/technical/arquitectura/01_MEGA_WORKFLOW_1_CAPTURA.md) | Lead Lifecycle detallado |
| **MW#2 Retención** | [/automation/docs/technical/arquitectura/02_MEGA_WORKFLOW_2_RETENCION.md](../../automation/docs/technical/arquitectura/02_MEGA_WORKFLOW_2_RETENCION.md) | Cliente a recompra |
| **MW#3 SEO** | [/automation/docs/technical/arquitectura/03_MEGA_WORKFLOW_3_SEO.md](../../automation/docs/technical/arquitectura/03_MEGA_WORKFLOW_3_SEO.md) | Fábrica de contenido |
| **Status MW1** | [/automation/workflows/MW1_LEAD_LIFECYCLE/STATUS.md](../../automation/workflows/MW1_LEAD_LIFECYCLE/STATUS.md) | Estado actual desarrollo |
| Arquitectura Funcional | [ARQUITECTURA_FUNCIONAL.md](ARQUITECTURA_FUNCIONAL.md) | Mapeo microservicios |
| Guía Integración | [../development/GUIA_INTEGRACION_MARKETING.md](../development/GUIA_INTEGRACION_MARKETING.md) | Para desarrollador marketing |

---

**Última Actualización**: 21 de Enero, 2026 - 11:30 COT
*Documento de integración entre plataforma web y sistema de automatización n8n*
