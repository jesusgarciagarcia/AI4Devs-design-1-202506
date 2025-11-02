## **A. Resumen del contexto**

El documento describe a **LTI**, una plataforma que redefine el concepto de ATS (Applicant Tracking System) tradicional mediante un enfoque **inteligente, colaborativo y predictivo**. Su objetivo es transformar la gestión del talento en una **experiencia orquestada**, combinando **IA contextual, automatización no-code y colaboración en tiempo real**.

### **Actores principales**

* **Reclutadores (HR):** responsables de la gestión del pipeline y comunicación con candidatos.
* **Hiring Managers:** decisores que evalúan y seleccionan candidatos.
* **Candidatos:** usuarios externos que interactúan con la empresa durante el proceso de selección.
* **C-Level / Dirección:** interesados en la visibilidad estratégica y KPIs del proceso.

### **Desafíos identificados**

1. **Experiencia fragmentada:** los sistemas actuales no se integran con las herramientas diarias.
2. **Baja colaboración:** los equipos no trabajan en tiempo real ni de forma transparente.
3. **Tareas repetitivas:** la operativa consume tiempo no productivo.
4. **Falta de inteligencia contextual:** no hay sistemas que comprendan las relaciones entre vacante y perfil.
5. **Poca analítica predictiva:** se carece de métricas accionables que mejoren decisiones.

En este contexto, el MVP debe centrarse en **resolver los principales puntos de fricción del flujo de reclutamiento**: gestión de candidatos, coordinación de entrevistas y priorización de talento.

---

## **B. Criterios de priorización**

Los tres casos de uso seleccionados se basan en los siguientes criterios:

| Criterio                       | Descripción                                                            | Peso  |
| ------------------------------ | ---------------------------------------------------------------------- | ----- |
| **Valor inmediato**            | Impacto directo en la eficiencia y experiencia del usuario.            | Alto  |
| **Viabilidad técnica**         | Implementable con tecnologías estándar y sin dependencias críticas.    | Alto  |
| **Aprendizaje validable**      | Permite medir engagement, reducción de tiempos o mejora de conversión. | Alto  |
| **Diferenciación competitiva** | Aporta elementos únicos frente a ATS tradicionales.                    | Medio |
| **Escalabilidad futura**       | Base sólida para extender funcionalidades de IA y colaboración.        | Medio |

Los casos elegidos equilibran **impacto**, **facilidad de desarrollo** y **validación temprana del modelo de negocio**.

---

## **C. Casos de uso priorizados**

---

### **Caso de uso #1 – Smart Pipelines (Gestión dinámica de procesos de selección)**

* **Objetivo:**
  Permitir a los equipos de HR gestionar candidatos mediante **pipelines inteligentes y configurables**, eliminando tareas manuales y adaptándose automáticamente a los distintos tipos de vacantes.

* **Actores:**
  Reclutador, Hiring Manager, Sistema LTI.

* **Precondiciones:**
  Vacante creada y candidatos asignados a un proceso de selección.

* **Flujo principal:**

  1. El reclutador define una vacante o selecciona una plantilla existente.
  2. LTI genera automáticamente un pipeline con etapas sugeridas según el rol.
  3. Cuando un candidato cambia de estado, el sistema ejecuta acciones automáticas (programar entrevista, enviar correo, actualizar métricas).
  4. El Hiring Manager visualiza el avance y puede dejar comentarios o valoraciones.

* **Flujos alternativos o excepciones:**

  * Si no hay disponibilidad de entrevistadores, el sistema propone reprogramación.
  * Si un candidato es descartado, se activa un flujo de feedback automático.

* **Resultado esperado:**
  Reducción del tiempo de gestión operativa y mejora en la trazabilidad de candidatos.

* **Valor para el MVP:**
  Es el **núcleo funcional del ATS**, imprescindible para validar la propuesta de eficiencia y automatización inteligente.

---

### **Caso de uso #2 – AI Recruiter Assistant (Asistente de reclutamiento basado en IA)**

* **Objetivo:**
  Asistir a los reclutadores en tareas clave mediante un **asistente conversacional** capaz de crear vacantes, analizar CVs y redactar comunicaciones automáticamente.

* **Actores:**
  Reclutador, Sistema LTI (IA contextual).

* **Precondiciones:**
  Acceso al espacio de trabajo LTI y permisos para crear o editar vacantes.

* **Flujo principal:**

  1. El usuario invoca al asistente (chat o comando).
  2. Solicita: “Crea una vacante para Full Stack Developer con base en las últimas contrataciones”.
  3. El asistente analiza los patrones anteriores y genera la descripción, requisitos y pipeline inicial.
  4. El reclutador revisa y aprueba el contenido antes de publicarlo.

* **Flujos alternativos o excepciones:**

  * Si la IA no encuentra patrones válidos, genera una plantilla genérica editable.
  * Si hay información incompleta, solicita aclaraciones al usuario.

* **Resultado esperado:**
  Creación de vacantes hasta un **50% más rápida** y reducción de errores o inconsistencias en descripciones.

* **Valor para el MVP:**
  Permite **demostrar la capa cognitiva del producto** y su propuesta diferenciadora: un ATS que asiste, no solo registra.

---

### **Caso de uso #3 – Collaborative Hiring Feed (Colaboración en tiempo real)**

* **Objetivo:**
  Facilitar la comunicación fluida entre los miembros del equipo de contratación mediante un **feed colaborativo en tiempo real** que centraliza actividades, comentarios y decisiones.

* **Actores:**
  HR, Hiring Managers, C-Level, IA de resumen.

* **Precondiciones:**
  Usuarios registrados con acceso al proceso de contratación y permisos adecuados.

* **Flujo principal:**

  1. Cada cambio en el proceso (nuevo candidato, avance de etapa, comentario, entrevista programada) se refleja en el feed.
  2. Los miembros pueden reaccionar, comentar o votar directamente sobre candidatos.
  3. La IA genera un **resumen contextual** de decisiones y sugerencias.

* **Flujos alternativos o excepciones:**

  * Si hay conflictos o evaluaciones contradictorias, el sistema notifica al equipo y propone una reunión o consenso.
  * Si un miembro está inactivo, puede recibir notificaciones asincrónicas por Slack o correo.

* **Resultado esperado:**
  Mayor participación del equipo y reducción del **30% en el tiempo de decisión** sobre contrataciones.

* **Valor para el MVP:**
  Representa el **pilar colaborativo del producto**, clave para validar el enfoque “reclutamiento como trabajo en equipo”.

---

## **D. Justificación y enfoque MVP**

Estos tres casos son **estratégicos y mínimos** porque:

1. **Validan la propuesta de valor completa:** combinan **automatización (Smart Pipelines)**, **asistencia inteligente (AI Recruiter)** y **colaboración (Hiring Feed)**, los tres pilares diferenciales de LTI.
2. **Son técnicamente viables en una primera fase:** pueden construirse sobre una arquitectura modular con servicios básicos de autenticación, base de datos y API.
3. **Generan métricas de validación temprana:**

   * **Engagement del usuario:** frecuencia de interacción con el asistente y el feed.
   * **Eficiencia operativa:** reducción de tiempo medio por vacante o tarea.
   * **Tasa de adopción:** número de usuarios activos por equipo o pipeline.
   * **Conversión:** incremento del ratio entrevista→contratación.

Con estos datos, el equipo puede validar la **hipótesis de mejora de productividad y colaboración** sin necesidad de desarrollar funciones complejas (como analítica avanzada o marketplace).

---

## **E. Recomendaciones adicionales**

### **Extensiones futuras**

1. **Predictive Candidate Matching:** integrar IA que priorice automáticamente candidatos según afinidad.
2. **Smart Briefing Rooms:** generar espacios previos a entrevistas con contexto y sugerencias.
3. **Bias Guardian / Sentiment Analysis:** implementar IA ética y explicable para evitar sesgos.
4. **Talent Graph AI:** conectar patrones históricos y descubrir perfiles ocultos.

### **Dependencias técnicas**

* Integraciones mínimas iniciales: Gmail/Outlook (para correos), Google Calendar/Microsoft 365 (para entrevistas), y Slack/Teams (para notificaciones).
* Infraestructura orientada a eventos y APIs abiertas para escalabilidad.
* Módulo de autenticación y roles para diferenciar HR, manager y candidato.

### **Límites del MVP**

**Incluye:**

* Creación y gestión dinámica de pipelines.
* Asistente IA básico con prompts preentrenados.
* Feed colaborativo con comentarios y reacciones.

**No incluye (fase posterior):**

* Matching predictivo avanzado.
* Analítica comparativa o benchmarking.
* Marketplace de integraciones externas.

---

✅ **Conclusión:**
El **MVP de LTI** debe centrarse en **automatizar, asistir y conectar**:

* **Automatizar** los procesos mediante *Smart Pipelines*.
* **Asistir** al usuario con el *AI Recruiter Assistant*.
* **Conectar** equipos con el *Hiring Feed*.

Estos tres casos permiten **validar la visión de LTI** —un ATS que piensa, colabora y aprende— con un alcance técnico realista y un potencial de diferenciación inmediato.
