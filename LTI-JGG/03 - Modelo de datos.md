## A. Análisis del dominio

**Propósito general del sistema (MVP).** Dar soporte a tres flujos troncales:

1. **Smart Pipelines** para gestionar procesos de selección con etapas configurables y acciones automáticas al cambiar de estado.
2. **AI Recruiter Assistant** para acelerar la creación de vacantes y artefactos (JD, emails, resúmenes).
3. **Collaborative Hiring Feed** para coordinar decisiones y comunicación en tiempo real entre HR y managers.

**Actores y objetos clave.**

* **Recruiter (HR)** y **Hiring Manager** (usuarios internos).
* **Candidato** (externo).
* **IA del sistema** (genera artefactos y resúmenes).
* **Dirección** (consumo mínimo de KPIs en MVP).

**Eventos o interacciones que crean/modifican datos.**

* Creación/edición/publicación de **JobPosting** (manual o asistida por IA).
* **Application** a una vacante y **transiciones** entre etapas del pipeline.
* **Programación de entrevistas** y captura de **evaluaciones/scorecards**.
* **Actividad colaborativa** (feed, comentarios, reacciones, decisiones).
* **Acciones automáticas** (notificaciones, creación de entrevistas, actualizaciones).

> **Suposiciones explícitas (MVP):** multi-tenant lógico por **Organization**; un **Pipeline** por **JobPosting**; automatizaciones en versión “lite” (triggers simples y pocas acciones); IA como generadora de artefactos textuales y resúmenes, sin modelos de matching avanzados.

---

## B. Identificación de entidades

| Entidad                  | Descripción                                    | Tipo               | Persistencia |
| ------------------------ | ---------------------------------------------- | ------------------ | ------------ |
| **Organization**         | Tenancy/empresa cliente                        | Principal          | Sí           |
| **User**                 | Usuario interno (HR, Manager, Admin)           | Principal          | Sí           |
| **Role** / **UserRole**  | Rol y asignación usuarios↔roles                | Referencia/Soporte | Sí           |
| **Candidate**            | Persona candidata                              | Principal          | Sí           |
| **JobPosting**           | Vacante publicada                              | Principal          | Sí           |
| **Pipeline**             | Flujo 1:1 asociado a la vacante                | Principal          | Sí           |
| **PipelineStage**        | Etapas ordenadas del pipeline                  | Principal          | Sí           |
| **Application**          | Candidatura a una vacante                      | Principal          | Sí           |
| **StageTransition**      | Evento de cambio de etapa                      | Soporte            | Sí           |
| **Interview**            | Entrevista (fecha/hora/estado)                 | Soporte            | Sí           |
| **InterviewInterviewer** | Puente Entrevista↔Entrevistadores              | Soporte            | Sí           |
| **Evaluation**           | Scorecard/valoración por usuario               | Soporte            | Sí           |
| **FeedEvent**            | Evento visible en el Hiring Feed               | Principal          | Sí           |
| **Comment**              | Comentario sobre feed/application              | Soporte            | Sí           |
| **Reaction**             | Reacción ligera (👍,✅)                         | Soporte            | Sí           |
| **AIArtifact**           | Artefacto generado por IA (JD, email, resumen) | Soporte            | Sí           |
| **AutomationRule**       | Regla trigger→acciones (lite)                  | Soporte            | Sí           |
| **Notification**         | Notificación emitida (email/Slack)             | Soporte            | Sí           |
| **Attachment**           | Fichero (CV, portfolio)                        | Soporte            | Sí           |
| **CalendarAccount**      | Conexión de calendario de User                 | Soporte            | Sí           |

---

## C. Definición del modelo lógico (relacional)

> Tipos sugeridos: `uuid`, `string (<=255)`, `text`, `int`, `smallint`, `bool`, `datetime`, `jsonb`. Claves *PK* primarias y *FK* foráneas.

### Núcleo organizacional y acceso

**Entidad:** `Organization`

* **Campos:** `OrganizationId (uuid, PK)`, `Name (string)`, `Domain (string, null)`, `CreatedAt (datetime)`
* **Notas:** Tenancy lógico; todas las entidades de negocio referencian `OrganizationId`.

**Entidad:** `User`

* **Campos:** `UserId (uuid, PK)`, `OrganizationId (uuid, FK)`, `Email (string, unique within org)`, `FullName (string)`, `Active (bool)`, `CreatedAt (datetime)`
* **Relación:** Organization 1:N User.

**Entidad:** `Role`, `UserRole`

* **Role:** `RoleId (smallint, PK)`, `Name (enum: Admin, HR, Manager, Exec)`
* **UserRole:** `(UserId (FK), RoleId (FK)) PK compuesto`

### Talento, vacantes y pipeline

**Entidad:** `Candidate`

* **Campos:** `CandidateId (uuid, PK)`, `FullName (string)`, `Email (string)`, `Phone (string, null)`, `Location (string, null)`, `CreatedAt (datetime)`
* **Notas:** Adjuntos (CV, portfolio) en `Attachment`.

**Entidad:** `JobPosting`

* **Campos:** `JobPostingId (uuid, PK)`, `OrganizationId (uuid, FK)`, `Title (string)`, `Description (text)`, `Department (string, null)`, `Seniority (enum)`, `Status (enum: Draft, Open, Paused, Closed)`, `CreatedBy (uuid, FK→User)`, `CreatedAt (datetime)`, `PublishedAt (datetime, null)`
* **Notas:** `Description` puede tener **traza a IA** mediante `AIArtifact`.

**Entidad:** `Pipeline`

* **Campos:** `PipelineId (uuid, PK)`, `JobPostingId (uuid, FK, unique)`, `Name (string)`, `CreatedAt (datetime)`
* **Cardinalidad:** JobPosting 1:1 Pipeline (MVP).

**Entidad:** `PipelineStage`

* **Campos:** `StageId (uuid, PK)`, `PipelineId (uuid, FK)`, `Name (string)`, `Type (enum: Screening, HR, Technical, Final, Offer, …)`, `OrderIndex (int)`
* **Cardinalidad:** Pipeline 1:N PipelineStage.

### Candidaturas, transiciones y entrevistas

**Entidad:** `Application`

* **Campos:** `ApplicationId (uuid, PK)`, `CandidateId (uuid, FK)`, `JobPostingId (uuid, FK)`, `Source (string, null)`, `CurrentStageId (uuid, FK→PipelineStage)`, `Status (enum: InProgress, Rejected, Hired, Withdrawn)`, `CreatedAt (datetime)`
* **Notas:** `CurrentStageId` denormalizado para lectura; el histórico vive en `StageTransition`.

**Entidad:** `StageTransition`

* **Campos:** `TransitionId (uuid, PK)`, `ApplicationId (uuid, FK)`, `FromStageId (uuid, null)`, `ToStageId (uuid, FK)`, `ChangedBy (uuid, FK→User)`, `Reason (string, null)`, `OccurredAt (datetime)`
* **Notas:** Evento canónico que dispara **AutomationRule**, **FeedEvent** y **Notification**.

**Entidad:** `Interview`

* **Campos:** `InterviewId (uuid, PK)`, `ApplicationId (uuid, FK)`, `StageId (uuid, FK)`, `ScheduledStart (datetime)`, `ScheduledEnd (datetime)`, `Location (string|url, null)`, `Status (enum: Scheduled, Completed, Canceled)`, `CreatedBy (uuid, FK→User)`
* **Notas:** Prepara el camino para auto-scheduling futuro.

**Entidad:** `InterviewInterviewer` (puente N:M)

* **Campos:** `InterviewId (uuid, FK)`, `UserId (uuid, FK)`; **PK compuesto** `(InterviewId, UserId)`

**Entidad:** `Evaluation`

* **Campos:** `EvaluationId (uuid, PK)`, `ApplicationId (uuid, FK)`, `ByUserId (uuid, FK→User)`, `StageId (uuid, FK)`, `Score (smallint 0..5)`, `Dimensions (jsonb)`, `Notes (text)`, `CreatedAt (datetime)`
* **Notas:** Múltiples evaluaciones por etapa/usuario; `Dimensions` permite rubricar sin sobrediseñar tablas.

### Colaboración, IA y automatización

**Entidad:** `FeedEvent`

* **Campos:** `FeedEventId (uuid, PK)`, `OrganizationId (uuid, FK)`, `ScopeType (enum: JobPosting|Application|Candidate)`, `ScopeId (uuid)`, `EventType (enum: StageChanged|InterviewScheduled|EvaluationSubmitted|CommentAdded|StatusChanged|AutomationFired|NotificationSent)`, `Payload (jsonb)`, `ActorUserId (uuid, FK→User, null si sistema)`, `OccurredAt (datetime)`
* **Notas:** Modelo de **evento genérico** para el Hiring Feed.

**Entidad:** `Comment`

* **Campos:** `CommentId (uuid, PK)`, `FeedEventId (uuid, FK, null)`, `ScopeType (enum)`, `ScopeId (uuid)`, `AuthorUserId (uuid, FK→User)`, `Body (text)`, `CreatedAt (datetime)`
* **Notas:** Permite comentar sobre un evento o sobre el recurso (por ejemplo, la Application).

**Entidad:** `Reaction`

* **Campos:** `ReactionId (uuid, PK)`, `TargetType (enum: FeedEvent|Comment)`, `TargetId (uuid)`, `UserId (uuid, FK)`, `Kind (enum: thumbs_up|check|heart|flag)`, `CreatedAt (datetime)`
* **Notas:** Reacciones ligeras para consenso rápido.

**Entidad:** `AIArtifact`

* **Campos:** `AIArtifactId (uuid, PK)`, `OrganizationId (uuid, FK)`, `Kind (enum: JobDescription|EmailDraft|CandidateSummary|FeedSummary)`, `SourceType (enum: JobPosting|Application|Candidate|Feed)`, `SourceId (uuid)`, `Prompt (text)`, `Output (text)`, `CreatedBy (uuid, FK→User|null si sistema)`, `CreatedAt (datetime)`
* **Notas:** Trazabilidad y auditabilidad de generación IA dentro del MVP.

**Entidad:** `AutomationRule` (versión “lite”)

* **Campos:** `AutomationRuleId (uuid, PK)`, `OrganizationId (uuid, FK)`, `Name (string)`, `IsActive (bool)`, `Trigger (enum: OnStageEnter|OnStageLeave|OnStatusChange)`, `TriggerStageId (uuid, FK→PipelineStage, null)`, `Actions (jsonb)`
* **Notas:** `Actions` contenidas (p. ej., `["create_interview","notify_slack","email_candidate"]`). Sin orquestaciones complejas.

**Entidad:** `Notification`

* **Campos:** `NotificationId (uuid, PK)`, `OrganizationId (uuid, FK)`, `Channel (enum: Email|Slack)`, `Target (string)`, `Subject (string)`, `Body (text)`, `RelatedType (enum)`, `RelatedId (uuid)`, `SentAt (datetime)`, `Status (enum: Sent|Failed)`
* **Notas:** Registro operativo; desde automatización o acción manual.

### Adjuntos y calendario

**Entidad:** `Attachment`

* **Campos:** `AttachmentId (uuid, PK)`, `OrganizationId (uuid, FK)`, `OwnerType (enum: Candidate|Application|JobPosting)`, `OwnerId (uuid)`, `FileName (string)`, `MimeType (string)`, `SizeBytes (int)`, `Url (string)`, `UploadedAt (datetime)`

**Entidad:** `CalendarAccount`

* **Campos:** `CalendarAccountId (uuid, PK)`, `UserId (uuid, FK)`, `Provider (enum: Google|Microsoft)`, `ExternalAccountId (string)`, `ConnectedAt (datetime)`
* **Notas:** Soporte básico de programación de entrevistas (no incluye slots ni busy times en MVP).

---

### Diagrama ER (textual)

```
Organization 1─* User
User *─* Role (via UserRole)

Organization 1─* JobPosting 1─1 Pipeline 1─* PipelineStage
Candidate 1─* Application *─1 JobPosting
Application 1─* StageTransition
Application 1─* Interview *─* User (via InterviewInterviewer)
Application 1─* Evaluation (* StageId, ByUserId)
Application 1─* FeedEvent (scope puede ser también JobPosting o Candidate)
FeedEvent 1─* Comment ; (Comment) *─* Reaction ; (FeedEvent) *─* Reaction

AIArtifact *─1 (scoped to: JobPosting|Application|Candidate|Feed)
AutomationRule *─1 Organization  → dispara → Notification (0..*)
Attachment *─1 (Candidate|Application|JobPosting)
User 1─* Notification
User 1─* AIArtifact (CreatedBy opcional)
User 1─* StageTransition (ChangedBy)
```

---

## D. Relaciones entre entidades (claves)

1. **JobPosting—Pipeline—PipelineStage** *(composición)*

   * Un `Pipeline` pertenece a una `JobPosting` y define sus `PipelineStage` ordenadas.
   * **Propósito:** materializar *Smart Pipelines* en el dominio.
   * **Impacto MVP:** habilita acciones por etapa y transiciones consistentes.

2. **Candidate—Application—JobPosting** *(asociación)*

   * Un `Candidate` puede tener múltiples `Application` a distintas `JobPosting`.
   * **Propósito:** representar postulaciones y su estado.
   * **Impacto:** base del embudo; métrica de conversión por vacante.

3. **Application—StageTransition—PipelineStage** *(evento de dominio)*

   * Cada cambio de `Stage` genera un `StageTransition`.
   * **Propósito:** **histórico auditable**, disparo de `AutomationRule`, creación de `FeedEvent`.
   * **Impacto:** núcleo para automatizar “programar entrevista”, “notificar”, “actualizar estado”.

4. **Interview—InterviewInterviewer—User** *(asociación N:M)*

   * Una `Interview` puede involucrar a varios entrevistadores; se vincula a `Application` y `Stage`.
   * **Impacto:** soporte inmediato a la coordinación de entrevistas.

5. **Evaluation—Application—User—Stage** *(dependencia contextual)*

   * Evaluaciones por usuario y etapa, con `Dimensions (jsonb)` para rubricar sin sobrediseño.
   * **Impacto:** input clave para decisiones en el `Feed`.

6. **FeedEvent—Comment—Reaction** *(agregación colaborativa)*

   * `FeedEvent` agrega actividad (transiciones, evaluaciones, notas); comentarios y reacciones construyen consenso.
   * **Impacto:** sustenta el **Collaborative Hiring Feed**.

7. **AIArtifact—(JobPosting|Application|Candidate|Feed)** *(trazabilidad IA)*

   * Mantiene prompts y outputs generados.
   * **Impacto:** evidencia de valor del **AI Assistant** y base para explicabilidad.

8. **AutomationRule—StageTransition → Notification / Interview** *(reglas simples)*

   * Reglas activadas por `Trigger` (p. ej. `OnStageEnter` con `TriggerStageId`) ejecutan `Actions`.
   * **Impacto:** automatización mínima viable sin motor de flujos complejo.

---

## E. Justificación técnica

**Ajuste al alcance MVP.**

* **Simplicidad:** El modelo privilegia **entidades canónicas** (JobPosting, Pipeline/Stage, Candidate, Application, Transition, Interview, Evaluation) con **FeedEvent** como “cinta transportadora” de actividad.
* **Normalización controlada:** Historial en `StageTransition`; denormalización táctica (`Application.CurrentStageId`) para lecturas rápidas.
* **Extensibilidad:**

  * **IA:** `AIArtifact` desacopla la generación respecto a los recursos de negocio.
  * **Automatización:** `AutomationRule` + `Actions (jsonb)` evita diseñar un DSL complejo; permite crecer a un orquestador.
  * **Colaboración:** `FeedEvent` con `Payload (jsonb)` absorbe nuevas clases de eventos sin migraciones agresivas.

**Simplificaciones concretas para el MVP.**

* Un **Pipeline** por **JobPosting** (sin librería global de plantillas; se puede clonar registros).
* `AutomationRule` con 2–3 **triggers** y 3–4 **acciones** predefinidas.
* Calendario en modo **conexión mínima** (`CalendarAccount` + datos de entrevista), sin sincronización de disponibilidad.
* `Evaluation.Dimensions (jsonb)` en lugar de tablas por criterio/dimensión.

**Extensiones futuras naturales.**

* **Biblioteca de Pipelines** reutilizables por rol/seniority; versionado de pipelines.
* **Matching Predictivo** (nuevas entidades para features de perfil y explicabilidad).
* **Briefing Rooms** (agregados de contexto/artefactos para una entrevista).
* **Auditoría y cumplimiento** (tabla de `AuditTrail`, anonimización/retención por políticas).
* **Integraciones profundas** (sincronización bidireccional con Slack/Teams/Calendars y LinkedIn/GitHub).

**Riesgos y cómo se mitigan.**

* **Crecimiento del Feed**: indexación por `ScopeType/ScopeId/OccurredAt` y archivado por ventana temporal.
* **Acciones de automatización**: colas idempotentes (garantizar exactamente-una-vez a nivel de aplicación).
* **Evolución de evaluaciones**: `Dimensions (jsonb)` controlada con validación de esquema a nivel app.

---

### Apéndice: Esquemas sintéticos (DDL orientativo)

```sql
-- Núcleo de pipeline
CREATE TABLE PipelineStage (
  StageId uuid PRIMARY KEY,
  PipelineId uuid NOT NULL REFERENCES Pipeline(PipelineId),
  Name varchar(120) NOT NULL,
  Type varchar(40) NOT NULL,
  OrderIndex int NOT NULL
);

CREATE TABLE Application (
  ApplicationId uuid PRIMARY KEY,
  CandidateId uuid NOT NULL REFERENCES Candidate(CandidateId),
  JobPostingId uuid NOT NULL REFERENCES JobPosting(JobPostingId),
  Source varchar(80),
  CurrentStageId uuid REFERENCES PipelineStage(StageId),
  Status varchar(20) NOT NULL,
  CreatedAt timestamptz NOT NULL
);

CREATE TABLE StageTransition (
  TransitionId uuid PRIMARY KEY,
  ApplicationId uuid NOT NULL REFERENCES Application(ApplicationId),
  FromStageId uuid,
  ToStageId uuid NOT NULL REFERENCES PipelineStage(StageId),
  ChangedBy uuid NOT NULL REFERENCES "User"(UserId),
  Reason varchar(240),
  OccurredAt timestamptz NOT NULL
);
```

---

**Conclusión.** El modelo propuesto **cubre íntegramente** los casos de uso del MVP: permite **operar el pipeline**, **colaborar en tiempo real** y **asistir con IA** con una base **normalizada, trazable y extensible**, minimizando complejidad prematura y dejando un camino claro para escalar en automatización, analítica e integraciones.
