# A. Visión general del sistema

**Propósito general.**
El sistema LTI (Lean Talent Intelligence) es un **ATS inteligente, colaborativo y asistido por IA** que permite a los equipos de reclutamiento gestionar de forma unificada los procesos de selección, automatizar tareas operativas y potenciar la toma de decisiones basada en contexto y datos.
Su MVP se centra en tres pilares funcionales:

1. **Smart Pipelines:** gestión dinámica de candidatos mediante etapas automatizables.
2. **AI Recruiter Assistant:** generación de artefactos de selección (JD, emails, resúmenes).
3. **Collaborative Hiring Feed:** espacio de colaboración en tiempo real entre HR y managers.

**Objetivos técnicos clave.**

* **Rapidez de validación** del producto mediante una arquitectura simple pero extensible.
* **Escalabilidad progresiva** (monolito modular con posible evolución a microservicios).
* **Interoperabilidad** con herramientas externas (Slack, Teams, calendarios, correo).
* **Observabilidad y trazabilidad** integradas desde el inicio.
* **Seguridad y multi-tenancy** garantizadas por diseño.

**Alcance del MVP.**
Incluye publicación de vacantes, postulaciones, pipeline y transiciones, entrevistas, evaluaciones, colaboración en el feed y generación de contenido con IA.
Quedan fuera de esta fase inicial: analítica predictiva avanzada, marketplace de integraciones, motor visual de automatizaciones y matching semántico completo.

---

## B. Componentes principales

| Componente                          | Descripción                                                                        | Tipo                    | Tecnologías sugeridas                                           | MVP |
| ----------------------------------- | ---------------------------------------------------------------------------------- | ----------------------- | --------------------------------------------------------------- | --- |
| **Frontend Web (SPA)**              | Interfaz para HR y managers, con dashboards, feed y edición colaborativa           | Presentación            | Next.js 15, React 19, TailwindCSS, SWR/React Query              | Sí  |
| **API Gateway / BFF**               | Enrutamiento HTTP y versión de API (`x-api-version`), control de CORS y throttling | Infraestructura backend | Nginx / ASP.NET 9 Minimal API                                   | Sí  |
| **Core Backend (Monolito Modular)** | Lógica de aplicación, dominio y persistencia del ATS                               | Servicio core           | .NET 9 (C#), MediatR, NHibernate, FluentMigrator, OpenTelemetry | Sí  |
| **Auth & Identity Service**         | Gestión de usuarios, roles y autenticación JWT (multi-tenant)                      | Infraestructura         | ASP.NET Identity / OpenIddict                                   | Sí  |
| **Notification Service**            | Envío de emails y mensajes (SMTP, Slack Webhook)                                   | Servicio auxiliar       | .NET Worker Service / RabbitMQ / SMTP                           | Sí  |
| **AI Artifact Generator**           | Generación de JD, resúmenes y emails mediante LLM externo                          | Servicio IA             | Python FastAPI + OpenAI API / Azure OpenAI                      | Sí  |
| **Scheduler / Automation Worker**   | Ejecución asíncrona de reglas y automatizaciones (OnStageEnter, etc.)              | Worker                  | Hangfire / MassTransit / RabbitMQ                               | Sí  |
| **Database**                        | Almacenamiento relacional de entidades del dominio                                 | Persistencia            | PostgreSQL 16                                                   | Sí  |
| **Blob Storage**                    | Archivos y adjuntos (CV, portfolios)                                               | Infraestructura         | AWS S3 / Azure Blob Storage                                     | Sí  |
| **Observability Stack**             | Logs, métricas, trazas distribuidas y health checks                                | Infraestructura         | OpenTelemetry, Prometheus, Grafana, Loki                        | Sí  |
| **Integration Layer (futuro)**      | Conectores con Slack, Google Calendar, LinkedIn, etc.                              | Extensión               | REST/Webhooks                                                   | No  |
| **Analytics & Insights Service**    | Analítica avanzada y dashboards predictivos                                        | Extensión               | ClickHouse / PowerBI Embedded                                   | No  |

---

## C. Arquitectura de alto nivel

```
                        ┌──────────────────────────────┐
                        │        Frontend Web (SPA)    │
                        │  React / Next.js / Tailwind  │
                        └─────────────┬────────────────┘
                                      │ HTTPS (REST/JSON)
                                      ▼
                 ┌──────────────────────────────┐
                 │      API Gateway / BFF       │
                 │  .NET 9 Minimal API + Auth   │
                 └─────────────┬────────────────┘
                               │
        ┌──────────────────────┼────────────────────────┐
        │                      │                        │
        ▼                      ▼                        ▼
┌───────────────────┐  ┌──────────────────┐  ┌──────────────────────┐
│  Application Core │  │ Notification Svc │  │   AI Artifact Svc    │
│  (.NET 9, DDD)    │  │ (.NET Worker)    │  │ (Python / FastAPI)   │
└────────┬──────────┘  └──────────────────┘  └──────────────────────┘
         │
         ▼
 ┌────────────────────────────┐
 │ PostgreSQL / NHibernate ORM│
 └────────────────────────────┘
         │
         ▼
 ┌────────────────────────────┐
 │     Blob / Object Storage  │
 └────────────────────────────┘
```

**Comunicación:**

* Síncrona (REST, JSON) entre frontend y backend.
* Asíncrona (event bus / RabbitMQ) para automatizaciones y notificaciones.
* API externa para IA y correo.

**Seguridad:**
Autenticación mediante JWT con *tenant claim* (`organization_id`). Autorización basada en roles y políticas (`[RequireAuthorization]`) por endpoint.

**Datos:**
Modelo relacional normalizado según entidades del dominio. Uso de transacciones unitarias y `Activity` para trazabilidad.

---

## D. Diseño por capas

### **1. Capa de presentación (Frontend)**

* Framework: **Next.js + React** para velocidad de iteración y compatibilidad SSR/SPA.
* Comunicación: **REST API** con token JWT.
* Principales vistas:

  * Dashboard por rol (HR, Manager).
  * Editor de vacantes y pipelines.
  * Feed colaborativo en tiempo real (WebSockets opcional MVP).
  * Formulario de aplicación de candidatos.

### **2. Capa de aplicación / APIs**

* Expone endpoints versionados (`/api/v1/*`) bajo API Gateway.
* Usa **MediatR** para desacoplar controladores y casos de uso.
* Gestiona flujos de negocio orquestados:
  `MoveCandidate → Create StageTransition → Trigger Automation → Publish FeedEvent`.
* Control de errores con **ProblemDetails** y trazas **OpenTelemetry**.
* Validaciones via FluentValidation.
* Soporte para **ActivitySource** en operaciones sensibles (transiciones, IA).

### **3. Capa de dominio**

* Modelado con **DDD ligero**: entidades, agregados y servicios de dominio.
* Agregados principales:

  * `JobPostingAggregate` (contiene `Pipeline` y `Stages`).
  * `ApplicationAggregate` (candidato, stage actual, transiciones, evaluaciones).
  * `FeedAggregate` (eventos, comentarios, reacciones).
* Eventos de dominio:

  * `StageTransitionOccurred`
  * `InterviewScheduled`
  * `EvaluationSubmitted`
  * `AutomationTriggered`
* Reglas de negocio encapsuladas en `Domain Services`.

### **4. Capa de infraestructura**

* Persistencia con **NHibernate + FluentMigrator** sobre PostgreSQL.
* Mensajería: **RabbitMQ** para colas de notificaciones y automatizaciones.
* Almacenamiento de archivos: **S3-compatible storage**.
* Observabilidad: **OpenTelemetry** para tracing y métricas.
* Configuración externa: `appsettings.json` + variables de entorno.

---

## E. Integraciones externas

| Integración                          | Propósito                                 | Tipo           | MVP |
| ------------------------------------ | ----------------------------------------- | -------------- | --- |
| **OpenAI / Azure OpenAI**            | Generación de descripciones y resúmenes   | REST API       | Sí  |
| **SMTP / SendGrid**                  | Envío de notificaciones de correo         | SMTP / API     | Sí  |
| **Slack Webhook**                    | Alertas de feed y automatizaciones        | Webhook        | Sí  |
| **Google / Microsoft Calendar**      | Programación básica de entrevistas        | OAuth + REST   | Sí  |
| **LinkedIn / GitHub / Behance**      | Enriquecimiento de candidatos             | REST / Scraper | No  |
| **Teams / Jira / Notion**            | Integraciones de colaboración corporativa | REST / SDK     | No  |
| **Analytics / PowerBI / ClickHouse** | Dashboards predictivos y benchmarking     | SQL / API      | No  |

---

## F. Decisiones técnicas y trade-offs

### **1. Estilo arquitectónico**

**Elegido:** Monolito modular (Clean Architecture).
**Alternativa:** Microservicios desde el inicio.
**Justificación:**

* Permite mayor velocidad de desarrollo y despliegue durante la validación del MVP.
* Se organiza por *bounded contexts* (Recruitment, Collaboration, Automation, AI) permitiendo futura separación física sin reescritura.
* Mínimo coste operativo y despliegue simple (Docker + single DB).

### **2. Persistencia**

**Elegido:** PostgreSQL + NHibernate.
**Alternativa:** Document DB (MongoDB).
**Justificación:** El modelo de datos es fuertemente relacional (candidatos, etapas, entrevistas, eventos). PostgreSQL garantiza integridad y consultas analíticas simples.

### **3. Comunicación**

**Elegido:** REST síncrono + cola asíncrona para eventos.
**Alternativa:** gRPC o Event Sourcing.
**Justificación:** REST simplifica el desarrollo inicial; la cola (RabbitMQ) habilita tareas de fondo y escalado progresivo.

### **4. IA y servicios externos**

**Elegido:** Externalización de IA mediante API (OpenAI/Azure).
**Alternativa:** Modelo interno fine-tuned.
**Justificación:** Reduce coste inicial y tiempo de entrenamiento; mantiene flexibilidad de proveedor.

### **5. Observabilidad**

**Elegido:** OpenTelemetry + Prometheus + Grafana.
**Justificación:** Nativo en .NET 9, fácil instrumentación y estandarización. Permite trazas distribuidas desde el MVP.

---

## G. Escalabilidad y evolución

| Eje                | MVP                               | Evolución prevista                     |
| ------------------ | --------------------------------- | -------------------------------------- |
| **Despliegue**     | Docker Compose / single container | Kubernetes (Helm + autoscaling)        |
| **Base de datos**  | PostgreSQL single node            | Replicación + particionamiento lógico  |
| **Mensajería**     | RabbitMQ simple                   | Event Bus (NATS / Kafka)               |
| **IA**             | LLM externo (OpenAI)              | Modelos híbridos (propios + externos)  |
| **Automatización** | Triggers básicos                  | Motor no-code visual + DSL de acciones |
| **Colaboración**   | Feed basado en polling            | WebSocket / EventStream en tiempo real |
| **Seguridad**      | JWT + tenant claim                | IdentityServer / OAuth2 federado       |
| **Analítica**      | Dashboards básicos                | Event warehouse + BI semántico         |

La arquitectura permite **escalar horizontalmente** el API Gateway, los Workers y los servicios IA.
Cada bounded context podrá **extraerse como microservicio** en fases de crecimiento sin romper contratos.

---

## H. Conclusión y recomendaciones

**Decisiones clave:**

* **Arquitectura monolítica modular** con patrones DDD y Clean Architecture.
* **Tecnologías unificadas en .NET 9 y React**, priorizando productividad.
* **Persistencia relacional** con integridad fuerte.
* **Observabilidad y automatización integradas** desde el MVP.
* **IA desacoplada** vía API externa para evitar deuda técnica temprana.

**Riesgos y mitigaciones:**

* *Riesgo:* sobrecarga de eventos y feed → *Mitigación:* indexación y archivado.
* *Riesgo:* complejidad de automatizaciones → *Mitigación:* limitar triggers a tres tipos.
* *Riesgo:* latencia en IA externa → *Mitigación:* caching de artefactos en BD.

**Recomendaciones de roadmap técnico:**

1. Fase 1 (0–3 meses): Implementar Core API, Smart Pipelines y Feed básico.
2. Fase 2 (3–6 meses): Añadir IA generativa y automatizaciones simples.
3. Fase 3 (6–12 meses): Introducir integraciones externas y analítica avanzada.
4. Fase 4 (12–18 meses): Escalado a microservicios y modelo de IA propio.

---

**Síntesis ejecutiva:**
La arquitectura propuesta para LTI combina **simplicidad inicial** con **capacidad de expansión natural**.
Construida sobre .NET 9, PostgreSQL y React, ofrece una **base moderna, trazable y segura**, perfectamente alineada con la visión de LTI:

> *Transformar el reclutamiento en una experiencia inteligente, colaborativa y asistida por IA.*
