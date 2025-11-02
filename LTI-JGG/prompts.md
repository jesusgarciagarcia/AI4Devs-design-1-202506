# Prompts

Para este ejercicio utilicé ChatGPT 5. Empecé por el uso de un meta prompting.
Mi estrategia para este ejercicio ha consistido en tener 3 chats principales:

1. Meta-prompting. He utilizado este chat para ir generando prompts para las diferentes fases de diseño del proyecto (análisis e investigación, casos de uso, modelo de datos y arquitectura general del proyecto).
2. Cada uno de los prompts generados, eran utilizados en ventanas de chats nuevas incluyendo como contexto los documentos generados en los chats anteriores.
3. Un último chat con todas las generaciones para generar el entregable del ejercicio.

Cada una de las respuestas se pueden encontrar en esta carpeta, enumeradas según la generación (NO coinciden que el número de prompt de este documento).

Quiero mencionar que como el primer prompt devuelve una investigación profunda, tengo que especificar que haga el análisis de un MVP para concretar la generación, aunque aún así, es demasiado extensa, aunque creo que la propuesta es muy buena y, por tanto, ambiciosa. Por ello, tuve que refinar el último prompt indicando que fuese más conciso y recordar que hablábamos de un MVP para obtener el resultado final.

## Prompt 1 - Meta-prompting inicial

Este es el primero de todos los chats.

``` markdown
Actúa como un experto en **ingeniería de prompts**. **Crea un Prompt** que incluya los siguientes elementos:

 1 - Instrucción, 2 - Estructura lógica, 3 - Claridad y precisión, 4 - Contexto adecuado, 5 - Formato de salida, 6 - Tono, estilo y longitud, 7 - Rol.

El contexto que el prompt es para un rol de product owner que está realizando una investigación y análisis de requisitos para una idea de negocio para la empresa LTI. LTI es una startup que quiere desarrollar el **ATS (Applicant-Tracking System)** del futuro.

Se tiene que solicitar las funcionalidades clave que harán brillar a LTI por encima de los competidores:

- Aumentar la eficiencia para los departamentos de HR
- Mejorar la colaboración en tiempo real entre reclutadores y managers
- Automatizaciones
- Asistencia de IA en diversas tareas

Además, se solicitará hacer **brainstorming** e investigar cuáles pueden ser las claves del éxito, y dejarlo plasmado para el resto del equipo
```

Después de una revisión, esa salida fue a un nuevo chat.

## Prompt 2 – Investigación y Análisis de Requisitos (Product Owner – LTI ATS)

```markdown

## 🧩 Rol
Eres un **Product Owner experto en tecnología, UX y reclutamiento digital**, trabajando en **LTI**, una startup que busca crear el **ATS (Applicant Tracking System) del futuro**.
Tu objetivo es **investigar, analizar y proponer funcionalidades clave** que diferencien a LTI en el mercado global de software de reclutamiento, combinando **eficiencia, colaboración y asistencia por IA**.

---

## 🧭 Instrucción
Tu tarea es elaborar un **análisis estratégico y funcional** del producto que LTI debe construir para liderar el sector ATS.
Debes realizar:
- **Investigación de mercado y benchmarking** contra competidores.
- **Brainstorming estructurado de ideas disruptivas.**
- **Propuesta de funcionalidades** alineadas con los pilares del producto:
  1. Eficiencia para departamentos de HR
  2. Colaboración en tiempo real entre reclutadores y managers
  3. Automatizaciones inteligentes
  4. Asistencia de IA en tareas de reclutamiento y análisis

Tu entrega debe servir como **documento base para el equipo de producto y dirección estratégica.**

---

## 🧠 Estructura lógica de salida

### **A. Contexto y objetivo**
- Describe brevemente la **visión de LTI** y el propósito del ATS.
- Explica los **problemas actuales de los sistemas ATS tradicionales** y por qué el mercado necesita una alternativa moderna.

### **B. Funcionalidades clave**
Identifica y describe las funcionalidades que impulsarán el éxito del producto.
Cada funcionalidad debe incluir:
- **Nombre y descripción.**
- **Propósito o problema que resuelve.**
- **Beneficio medible o indicador de éxito.**
- **Ejemplo práctico de uso.**

Estructura la sección en cuatro bloques:
1. **Eficiencia para HR.**
2. **Colaboración en tiempo real.**
3. **Automatizaciones inteligentes.**
4. **Asistencia de IA.**

### **C. Diferenciadores competitivos**
- Compara las ideas con ATS reconocidos (Lever, Greenhouse, Workable, Recruitee, etc.).
- Explica **qué hará destacar a LTI**:
  UX más ágil, IA contextual, predicción de talento, integración avanzada, etc.

### **D. Brainstorming de innovación**
Realiza una lluvia de ideas con **al menos 10 propuestas disruptivas** (ejemplo: matching predictivo, entrevistas simuladas por IA, feedback emocional, dashboards colaborativos).
Preséntalas en una **tabla con estas columnas**:

| Idea innovadora | Descripción breve | Impacto (Alto/Medio/Bajo) | Viabilidad técnica (Alta/Media/Baja) |

### **E. Claves del éxito**
Resume los **factores críticos de éxito** que permitirán a LTI destacar:
- Tecnología y arquitectura
- Experiencia del usuario
- IA y automatización
- Cumplimiento legal (GDPR, EEOC)
- Cultura de colaboración interna

Incluye **recomendaciones estratégicas** para las primeras fases del roadmap (MVP → Escalado → Expansión).

### **F. Conclusión ejecutiva**
Redacta un resumen final con:
- Las **3 propuestas de valor más fuertes** del ATS de LTI.
- Un cierre inspirador dirigido a **stakeholders e inversores**, resaltando la oportunidad de mercado.

---

## ✍️ Formato de salida
- Usa **títulos con `##`** y subtítulos claros.
- Utiliza **listas numeradas o con viñetas** para estructurar ideas.
- Usa **negritas** para resaltar términos clave.
- Presenta comparativas y clasificaciones en **tablas**.
- Longitud esperada: **1.500 a 2.000 palabras**.

---

## 🎨 Tono, estilo y longitud
- **Tono:** profesional, estratégico y visionario.
- **Estilo:** claro, estructurado y accesible tanto para perfiles técnicos como de negocio.
- **Extensión:** documento completo de análisis, no menos de 1.500 palabras.

---

## 🧱 Contexto adicional
- LTI es una **startup tecnológica** que busca revolucionar el reclutamiento mediante un sistema centrado en la **experiencia humana y la inteligencia artificial aplicada**.
- El público objetivo son **empresas medianas y grandes** que buscan **reducir el time-to-hire**, **mejorar la experiencia del candidato** y **optimizar la colaboración entre HR y managers**.

---

## 🧩 Ejemplo de inicio esperado
> **Visión de LTI**
> LTI nace con la misión de reinventar la manera en que las organizaciones descubren, evalúan y contratan talento. Su ATS no será solo una herramienta administrativa, sino un **sistema inteligente de orquestación del talento**, diseñado para eliminar fricciones, aumentar la eficiencia y crear experiencias humanas impulsadas por datos.

---

👉 **Inicia ahora tu análisis** siguiendo la estructura anterior y responde como si fueras el **Product Owner de LTI**, redactando el documento completo.

```

## Prompt 3 – Generación de Casos de Uso a partir de un Fichero de Contexto

```markdown
## 🧩 Rol
Eres un **Analista de Negocio y Product Owner Senior** especializado en **definición de requisitos funcionales** y diseño de **MVPs (Minimum Viable Products)** para startups tecnológicas.
Tu función es **analizar un fichero de contexto de investigación y objetivos** proporcionado y, a partir de su contenido, **extraer y desarrollar los 3 casos de uso más importantes** para el proyecto.

---

## 🎯 1. Instrucción
Lee atentamente el **fichero de contexto** y realiza un **análisis interpretativo profundo**.
Tu objetivo es **identificar los tres casos de uso más relevantes y viables** para una primera versión **MVP** del producto, centrando el esfuerzo en **máximo impacto con el mínimo desarrollo necesario**.

Debes:
- Detectar los **problemas clave** y **necesidades reales** mencionadas en el contexto.
- Formular **casos de uso claros, completos y orientados al usuario final**.
- Justificar por qué esos tres casos de uso son los más prioritarios para el MVP.
- Evitar casos secundarios o dependientes de otros módulos no esenciales.

---

## 🧠 2. Estructura lógica de salida

### **A. Resumen del contexto**
- Síntesis de los principales objetivos y hallazgos extraídos del fichero.
- Identificación de los actores clave, los usuarios objetivo y los desafíos actuales.

### **B. Criterios de priorización**
Explica brevemente los **criterios usados para seleccionar los tres casos de uso principales**, por ejemplo:
- Valor aportado al usuario.
- Viabilidad técnica en una primera iteración.
- Alineación con los objetivos de negocio y métricas del MVP.
- Capacidad de generar aprendizaje temprano (feedback loop).

### **C. Casos de uso priorizados**
Desarrolla **tres casos de uso principales** extraídos del fichero, **uno por bloque**, con esta estructura:

#### **Caso de uso #1 – [Nombre descriptivo]**
- **Objetivo:** qué problema o necesidad cubre.
- **Actores:** usuarios o sistemas involucrados.
- **Precondiciones:** requisitos o estado previo para ejecutarse.
- **Flujo principal:** pasos que sigue el usuario o el sistema.
- **Flujos alternativos o excepciones:** variaciones importantes.
- **Resultado esperado:** salida o cambio tras su ejecución.
- **Valor para el MVP:** por qué es esencial para la primera versión.

*(Repite esta estructura para los tres casos de uso más importantes.)*

### **D. Justificación y enfoque MVP**
- Explica por qué estos tres casos son **estratégicos y mínimos** para validar la propuesta de valor.
- Detalla qué métricas iniciales permitirán **validar el éxito del MVP** (por ejemplo: engagement, eficiencia, tiempo ahorrado, conversión, etc.).

### **E. Recomendaciones adicionales**
- Sugiere **posibles extensiones o iteraciones futuras** derivadas de los casos de uso principales.
- Indica si hay **dependencias técnicas o de negocio** a considerar.

---

## 🧾 3. Claridad y precisión
- Usa un lenguaje **preciso, estructurado y sin ambigüedades**.
- Evita tecnicismos innecesarios y escribe de forma comprensible para equipos mixtos (negocio, diseño, desarrollo).
- Define claramente los límites del MVP: qué **sí** y qué **no** incluiría.

---

## 🌐 4. Contexto adecuado
El contexto proviene de un **fichero de investigación y análisis de objetivos** sobre un nuevo producto (por ejemplo, un ATS, un SaaS o una aplicación interna).
Debes centrarte en **transformar hallazgos cualitativos y estratégicos** en **casos de uso funcionales y priorizados**, orientados al desarrollo de un **MVP validable**.

---

## 🧱 5. Formato de salida
- Usa **encabezados (`##`, `###`)** para estructurar cada bloque.
- Utiliza **listas** y **tablas** si es necesario para mostrar criterios o comparativas.
- Resalta conceptos clave con **negritas**.
- Extensión aproximada: **800 a 1.200 palabras**.

---

## 🗣️ 6. Tono, estilo y longitud
- **Tono:** analítico, profesional y centrado en producto.
- **Estilo:** claro, orientado a decisiones y con lenguaje de negocio.
- **Longitud:** suficiente para documentar el razonamiento sin redundancia.

---

## 👤 7. Rol e intención
Asume el rol de:
> **Analista de negocio / Product Owner de LTI**, encargado de definir los **casos de uso críticos para el MVP** a partir del fichero de contexto de investigación y objetivos.

Tu respuesta debe reflejar:
- Capacidad de síntesis y priorización.
- Enfoque MVP (valor máximo, esfuerzo mínimo).
- Mentalidad de producto centrada en el usuario.

---

## 🚀 Ejemplo de inicio esperado
> **Resumen del contexto**
> El documento de investigación revela una oportunidad de mercado para optimizar el flujo de selección de candidatos en empresas medianas, donde los procesos manuales y la falta de comunicación entre HR y managers generan demoras y errores.
>
> **Criterios de priorización:** Se priorizan casos que aporten valor inmediato a HR y managers, sean técnicamente factibles en corto plazo y permitan validar el impacto de la automatización y colaboración.
>
> **Caso de uso #1 – Creación y publicación rápida de vacantes**
> **Objetivo:** Permitir a los recruiters crear, aprobar y publicar vacantes en minutos, desde una única interfaz conectada a múltiples portales.
> ...

---

👉 **Inicia ahora tu análisis** aplicando esta estructura y extrayendo los **3 casos de uso principales** del fichero de contexto, con enfoque MVP.
```

## Prompt 4 – Generación del Modelo de Datos a partir de Casos de Uso

```markdown

## 🧩 Rol
Eres un **Arquitecto de Software y Diseñador de Modelos de Datos** especializado en **sistemas SaaS y productos MVP**.
Tu misión es **analizar los casos de uso funcionales proporcionados** y, a partir de ellos, **definir un modelo de datos coherente, normalizado y orientado al dominio del negocio**.

El objetivo es ofrecer una base sólida para el desarrollo de la primera versión **MVP** del producto, manteniendo un equilibrio entre **simplicidad, extensibilidad y alineación funcional**.

---

## 🎯 1. Instrucción
Lee atentamente los **casos de uso proporcionados** y **deriva un modelo de datos lógico** que:
- Cubra **todas las entidades necesarias** para soportar los flujos principales del MVP.
- Evite redundancias y mantenga la **coherencia de relaciones y cardinalidades**.
- Identifique las **entidades núcleo (core domain)** y las **entidades de soporte o referencia**.
- Incluya atributos esenciales, sin sobredimensionar el diseño para etapas futuras.

Tu respuesta debe incluir:
1. **Análisis conceptual** del dominio según los casos de uso.
2. **Modelo de datos lógico** (entidades, relaciones y atributos principales).
3. **Justificación técnica y funcional** de las decisiones de modelado.

---

## 🧠 2. Estructura lógica de salida

### **A. Análisis del dominio**
- Resume el propósito general del sistema según los casos de uso.
- Identifica los **actores y objetos de negocio** clave.
- Define los **eventos o interacciones principales** que originan o modifican datos.

### **B. Identificación de entidades**
- Lista las **entidades principales**, con una breve descripción de su rol.
- Incluye también las **entidades auxiliares o de referencia** necesarias (catálogos, configuraciones, logs, etc.).

Ejemplo de formato:
| Entidad | Descripción | Tipo | Persistencia (Sí/No) |
|----------|--------------|------|----------------------|
| Candidate | Persona que aplica a una vacante | Principal | Sí |
| JobPosting | Oferta publicada por la empresa | Principal | Sí |
| Interview | Evento de entrevista entre candidato y reclutador | Soporte | Sí |

### **C. Definición del modelo lógico**
Describe el **modelo lógico relacional o orientado a documentos**, según el tipo de aplicación (por defecto, modelo relacional).
Para cada entidad, especifica:

**Entidad:** `NombreEntidad`
- **Campos principales:** lista de atributos clave con tipo de dato sugerido (ej. string, int, datetime, bool).
- **Claves primarias / foráneas:** relaciones con otras entidades.
- **Cardinalidad:** 1:1, 1:N, N:M (si aplica).
- **Notas funcionales:** validaciones o reglas de negocio relevantes.

Incluye un **diagrama ER textual** o pseudográfico.

### **D. Relaciones entre entidades**
Explica las relaciones más relevantes, indicando:
- Tipo de relación (composición, asociación, dependencia).
- Propósito funcional.
- Impacto en el MVP (por qué es necesaria desde el punto de vista de los casos de uso).

### **E. Justificación técnica**
- Explica por qué el modelo propuesto es adecuado para el **alcance MVP**.
- Indica posibles simplificaciones para el MVP y extensiones futuras (por ejemplo: soporte multi-empresa, auditorías, IA, etc.).

---

## 🧾 3. Claridad y precisión
- Usa terminología de **modelado de datos y diseño de dominio**.
- Mantén nombres consistentes con los casos de uso (por ejemplo, “Vacante” → `JobPosting`).
- Evita añadir entidades no soportadas por los casos de uso actuales.
- Si hay ambigüedades, indica tus **suposiciones explícitamente**.

---

## 🌐 4. Contexto adecuado
El modelo de datos debe alinearse con los **casos de uso identificados para el MVP**.
Por tanto, el diseño debe:
- Reflejar el **core funcional mínimo viable**.
- Mantenerse **modular y extensible** para futuras versiones.
- Favorecer la **trazabilidad y consistencia** de la información.

---

## 🧱 5. Formato de salida
- Usa **encabezados (`##`, `###`)** y **tablas** para mayor claridad.
- Emplea **bloques de código** para representar estructuras de entidades, relaciones o diagramas ER.
- Utiliza **negritas** para destacar términos clave.
- Longitud esperada: **1.000 a 1.500 palabras**.

---

## 🗣️ 6. Tono, estilo y longitud
- **Tono:** técnico, estructurado y fundamentado.
- **Estilo:** profesional y didáctico, entendible tanto para desarrolladores como para Product Managers.
- **Longitud:** lo suficiente para describir la estructura y justificarla sin redundancias.

---

## 👤 7. Rol e intención
Asume el rol de:
> **Arquitecto de Datos de LTI**, responsable de diseñar el modelo de datos para el MVP del sistema descrito en los casos de uso.

Tu enfoque debe demostrar:
- Dominio en **diseño lógico de datos** y **modelado orientado al dominio**.
- Capacidad de **alinear la arquitectura de datos con los flujos funcionales**.
- Prioridad en **simplicidad y mantenibilidad** para el MVP.

---

## 🚀 Ejemplo de inicio esperado
> **Análisis del dominio**
> Los casos de uso describen un flujo central basado en la publicación de vacantes, recepción de candidatos y coordinación de entrevistas. El dominio se centra en tres actores principales: el reclutador, el manager y el candidato.
>
> **Entidades principales:** `Company`, `JobPosting`, `Candidate`, `Application`, `Interview`.
>
> **Modelo lógico:**
> - `JobPosting` (1:N) `Application`
> - `Application` (1:N) `Interview`
> - `Candidate` (1:N) `Application`
>
> **Justificación:** Este modelo cubre el 80% del flujo MVP con cinco tablas esenciales y sin dependencias externas. Permite validar los flujos de contratación iniciales y medir métricas de conversión por vacante.

---

👉 **Inicia ahora el diseño del modelo de datos** aplicando la estructura anterior y basándote en los casos de uso proporcionados.

```

## Prompt 5 – Diseño del Sistema y Arquitectura de Alto Nivel

```markdown
# 🧭 Prompt para ChatGPT – Diseño del Sistema y Arquitectura de Alto Nivel

## 🧩 Rol
Eres un **Arquitecto de Software Senior** especializado en **diseño de sistemas escalables y MVPs de productos SaaS**.
Tu misión es **diseñar la arquitectura de alto nivel** del sistema descrito en los **casos de uso y modelo de datos previos**, definiendo los **componentes principales, su interacción, y las decisiones técnicas clave** que permitirán construir un producto sólido, extensible y mantenible desde la fase MVP.

---

## 🎯 1. Instrucción
Analiza los **casos de uso y el modelo de datos** del proyecto, y elabora un **diseño arquitectónico de alto nivel** que:

1. Cubra los **flujos funcionales principales del MVP**.
2. Defina la **estructura modular** del sistema (capas, servicios, interfaces, integraciones).
3. Identifique los **componentes críticos** (backend, frontend, bases de datos, APIs, mensajería, autenticación, observabilidad, etc.).
4. Justifique las **decisiones técnicas** tomadas, considerando la escalabilidad, mantenibilidad y simplicidad propias de un MVP.
5. Proponga **evoluciones naturales** hacia una arquitectura más completa a futuro (por ejemplo, microservicios, IA, analítica, etc.).

---

## 🧠 2. Estructura lógica de salida

### **A. Visión general del sistema**
- Resume brevemente el propósito del sistema según los casos de uso.
- Define los **principales objetivos técnicos**: fiabilidad, escalabilidad, facilidad de integración, coste, velocidad de desarrollo.
- Identifica el **alcance del MVP**: qué funcionalidades se implementan en esta fase y cuáles se dejan para versiones posteriores.

### **B. Componentes principales**
Describe los módulos o bloques arquitectónicos principales y su rol dentro del sistema.
Ejemplo de estructura:

| Componente | Descripción | Tipo | Tecnologías sugeridas | MVP (Sí/No) |
|-------------|--------------|------|------------------------|--------------|
| API Gateway | Enrutamiento de peticiones y versionado | Backend infra | .NET 9 Minimal API / Nginx | Sí |
| Auth Service | Gestión de usuarios y permisos | Servicio core | IdentityServer / JWT | Sí |
| AI Assistant | Asistencia inteligente en selección | Servicio IA | Python / OpenAI API | No (futuro) |

### **C. Arquitectura de alto nivel**
Representa el **diseño global del sistema** mostrando los componentes y su interacción.
Incluye un **diagrama textual o ASCII** de arquitectura de alto nivel (ejemplo):

\ ```
[Frontend Web/App]
│
▼
[API Gateway] ──► [Application Layer] ──► [Domain Layer] ──► [Database]
│
├──► [Auth Service]
├──► [Notification Service]
└──► [External Integrations]

\ ````

Explica cómo se comunican los componentes (REST, gRPC, mensajería, eventos, etc.) y cómo se gestionan la seguridad y los datos.

### **D. Diseño por capas**
Detalla el **modelo en capas o módulos** del sistema, según corresponda:

- **Capa de presentación (Frontend):** canales de acceso del usuario, tipo de cliente, framework y comunicación con backend.
- **Capa de aplicación / APIs:** lógica de orquestación, endpoints, control de flujo.
- **Capa de dominio:** reglas de negocio, entidades, servicios de dominio.
- **Capa de infraestructura:** persistencia, mensajería, almacenamiento, logs, etc.

Incluye también cómo se implementarán **observabilidad**, **seguridad**, y **configuración**.

### **E. Integraciones externas**
Indica las **integraciones o dependencias externas** necesarias, especificando:
- Propósito (autenticación, analítica, almacenamiento, correo, IA, etc.).
- Tipo de integración (API REST, webhook, SDK, etc.).
- Relevancia para el MVP.

### **F. Decisiones técnicas y trade-offs**
Expón las **decisiones de diseño más importantes**, justificando la elección de tecnologías, patrones y estilos arquitectónicos (por ejemplo: monolito modular vs microservicios).
Incluye:
- Alternativas evaluadas.
- Beneficios y riesgos de la solución elegida.
- Criterios de priorización para MVP (rapidez, simplicidad, validación temprana).

### **G. Escalabilidad y evolución**
Explica cómo la arquitectura puede evolucionar desde el MVP hacia una solución más compleja:
- Escalado horizontal / vertical.
- Desacoplamiento progresivo.
- Incorporación de IA, analítica o event sourcing.
- Posible transición a una arquitectura de microservicios o hexagonal.

### **H. Conclusión y recomendaciones**
Cierra con una **síntesis ejecutiva**:
- Principales decisiones arquitectónicas.
- Riesgos o dependencias críticas.
- Recomendaciones para el equipo técnico y roadmap posterior.

---

## 🧾 3. Claridad y precisión
- Usa lenguaje **técnico claro y preciso**.
- Define los términos críticos (e.g., “Service Layer”, “Gateway”, “Event Bus”).
- Evita ambigüedades o suposiciones sin justificar.
- Si se hacen **suposiciones**, indícalas explícitamente.

---

## 🌐 4. Contexto adecuado
Este diseño debe **alinearse con los casos de uso y modelo de datos definidos previamente**.
El foco está en **el MVP**, no en la solución final completa:
- Priorizando la **rapidez de implementación y mantenimiento**.
- Reduciendo la complejidad técnica inicial.
- Permitiendo evolución sin reescribir el sistema.

---

## 🧱 5. Formato de salida
- Usa **encabezados (`##`, `###`)** y **tablas** para organizar los componentes.
- Incluye **diagramas ASCII o pseudográficos** para la arquitectura.
- Resalta decisiones clave con **negritas**.
- Longitud esperada: **1.500 a 2.000 palabras**.

---

## 🗣️ 6. Tono, estilo y longitud
- **Tono:** técnico, estratégico y fundamentado.
- **Estilo:** claro, modular y orientado a comunicación con stakeholders técnicos y de producto.
- **Longitud:** nivel documento de diseño (detallado pero legible).

---

## 👤 7. Rol e intención
Asume el rol de:
> **Arquitecto de Software de LTI**, encargado de definir la **arquitectura de alto nivel** del sistema, con foco en el **MVP** del ATS (Applicant Tracking System) del futuro.

Tu respuesta debe reflejar:
- Experiencia en **diseño de sistemas empresariales y MVPs escalables**.
- Conocimiento práctico de **arquitectura limpia, DDD y principios SOLID**.
- Capacidad para comunicar decisiones arquitectónicas a perfiles técnicos y de negocio.

---

## 🚀 Ejemplo de inicio esperado
> **Visión general del sistema**
> El sistema ATS de LTI tiene como objetivo optimizar la gestión del talento mediante automatización, colaboración y asistencia de IA. En su fase MVP, se enfocará en la publicación de vacantes, recepción de candidatos y coordinación de entrevistas.
>
> **Componentes principales:**
> - Frontend web SPA (Next.js + Tailwind)
> - Backend monolito modular (ASP.NET 9 Minimal API)
> - Base de datos PostgreSQL
> - Servicio de autenticación con JWT
> - Logging y trazabilidad con OpenTelemetry
>
> **Arquitectura de alto nivel:**
> ```
> [Frontend] → [API Gateway] → [Application Layer] → [Domain] → [PostgreSQL]
>                     │
>                     ├─► [Auth Service]
>                     └─► [Notification Queue]
> ```
>
> Esta arquitectura prioriza simplicidad y velocidad de entrega, permitiendo evolucionar hacia servicios independientes a medida que crece la carga y la funcionalidad.

---

👉 **Inicia ahora el diseño de la arquitectura de alto nivel**, aplicando la estructura anterior y centrando las decisiones en la **fase MVP del sistema**.
```

## Prompt 6 – Entregable de Diseño Inicial del Sistema LTI (Versión MVP)

```markdown

## 🧩 Rol
Eres un **Arquitecto de Producto y Software Senior**, con experiencia en diseño de sistemas SaaS, descubrimiento de producto y documentación técnica ejecutiva.
Tu misión es **diseñar y presentar la primera versión del sistema LTI (Applicant Tracking System del futuro)**, elaborando un **entregable completo** que resuma la visión, el modelo de negocio y los componentes técnicos clave del MVP.

---

## 🎯 1. Instrucción
Tu tarea consiste en **generar un documento integral** que combine visión de producto, diseño funcional y arquitectura técnica.
Debes crear un **entregable de presentación ejecutiva y técnica** que contenga los siguientes **artefactos**:

### **Artefactos obligatorios**
1. ✅ **Descripción breve del software LTI**
   - Explica qué es, qué problema resuelve y cuál es su **valor diferencial** frente a los ATS tradicionales.
   - Incluye su **propuesta de valor**, **ventajas competitivas** y alineación con la visión de la startup.

2. ✅ **Explicación de las funciones principales**
   - Detalla las **funcionalidades esenciales del MVP** derivadas de los casos de uso.
   - Incluye los módulos o áreas del sistema (por ejemplo: gestión de vacantes, seguimiento de candidatos, colaboración HR/manager, IA de soporte).

3. ✅ **Diagrama Lean Canvas**
   - Representa el modelo de negocio de LTI de forma esquemática.
   - Incluye los 9 bloques estándar: **Problema, Segmento de clientes, Propuesta de valor, Solución, Canales, Flujo de ingresos, Estructura de costes, Métricas clave y Ventaja competitiva**.
   - Puedes presentarlo como tabla o esquema visual en formato texto.

4. ✅ **Descripción de los 3 casos de uso principales**
   - Usa los casos de uso extraídos del análisis previo.
   - Para cada uno, incluye:
     - Objetivo
     - Actores
     - Flujo principal
     - Valor aportado
   - Acompaña cada uno con un **diagrama de flujo o secuencia textual** (ASCII o pseudográfico).

5. ✅ **Modelo de datos**
   - Expón las **entidades principales, sus atributos (nombre y tipo)** y las **relaciones entre ellas**.
   - Representa un **diagrama ER simplificado** en formato textual o tabla.

6. ✅ **Diseño del sistema a alto nivel**
   - Explica la **arquitectura general del sistema** (frontend, backend, base de datos, servicios, integraciones).
   - Incluye un **diagrama de arquitectura** (ASCII o pseudográfico).
   - Muestra cómo los componentes se comunican y soportan los casos de uso principales.

7. ✅ **Diagrama C4** (nivel de detalle en un componente elegido)
   - Elige un componente central (por ejemplo, “Gestión de Candidatos” o “Publicación de Vacantes”).
   - Desarrolla un **diagrama C4** con los niveles:
     - **C1:** Contexto general del sistema.
     - **C2:** Contenedores del componente elegido.
     - **C3:** Componentes internos y relaciones.
   - Acompaña con una breve explicación de cada nivel.

---

## 🧠 2. Estructura lógica de salida

### **A. Resumen ejecutivo**
- Descripción del software y objetivos estratégicos.
- Valor añadido y visión de impacto en el mercado.

### **B. Funciones principales**
- Descripción funcional y resumen modular (por bloques).

### **C. Lean Canvas**
- Representación esquemática o tabular de los 9 bloques.

### **D. Casos de uso**
- Descripción + diagrama para los tres casos clave del MVP.

### **E. Modelo de datos**
- Entidades, atributos y relaciones (tabla o diagrama ER).

### **F. Diseño del sistema (alto nivel)**
- Explicación general + diagrama de arquitectura.

### **G. Diagrama C4**
- Contexto → Contenedores → Componentes del subsistema seleccionado.

### **H. Conclusión**
- Síntesis final del valor técnico y de negocio del diseño.

---

## 🧾 3. Claridad y precisión
- Sé **estructurado y explícito**: cada sección debe ser fácilmente identificable.
- Emplea lenguaje **técnico y de negocio equilibrado**.
- Evita tecnicismos innecesarios, pero justifica decisiones clave.
- Si alguna información depende del contexto previo, indica tus **suposiciones**.

---

## 🌐 4. Contexto adecuado
El sistema LTI busca **redefinir los ATS tradicionales** mediante:
- **Eficiencia en HR**,
- **Colaboración en tiempo real**,
- **Automatización de flujos**,
- **Asistencia de IA para decisiones y matching**.

Este entregable se centra en la **versión MVP** del sistema, orientado a validar el **core funcional y técnico**, manteniendo flexibilidad para escalar a futuro.

---

## 🧱 5. Formato de salida
- Usa **encabezados (`##`, `###`)** y **tablas** para estructurar cada artefacto.
- Representa **diagramas** en formato ASCII o texto pseudográfico.
- Resalta elementos clave con **negritas**.
- Longitud recomendada: **2.000 a 3.000 palabras**.
- Presentación clara, legible y con jerarquía visual adecuada.

---

## 🗣️ 6. Tono, estilo y longitud
- **Tono:** profesional, ejecutivo y técnico.
- **Estilo:** estructurado, explicativo y persuasivo.
- **Longitud:** documento completo para revisión de producto y arquitectura.

---

## 👤 7. Rol e intención
Asume el rol de:
> **Arquitecto de Producto de LTI**, responsable de entregar la primera versión conceptual y técnica del sistema, incluyendo todos los artefactos requeridos para la revisión de dirección y desarrollo.

Tu respuesta debe demostrar:
- Visión estratégica de producto.
- Coherencia entre negocio, funcionalidad y técnica.
- Capacidad de comunicar diseño complejo de forma simple y clara.

---

## 🚀 Ejemplo de inicio esperado
> **Resumen ejecutivo**
> LTI es un sistema ATS de nueva generación que combina automatización, inteligencia artificial y colaboración en tiempo real para revolucionar la gestión del talento.
>
> Su propuesta de valor se basa en reducir el *time-to-hire* en más del 40% y ofrecer una experiencia integrada entre reclutadores, managers y candidatos.
>
> **Funciones principales:** gestión centralizada de vacantes, pipeline de candidatos, analítica inteligente y comunicación unificada.
>
> **Lean Canvas (resumen):**
> | Bloque | Descripción |
> |---------|--------------|
> | Problema | Procesos de selección lentos, desconectados y sin inteligencia predictiva. |
> | Solución | Plataforma colaborativa impulsada por IA. |
> | Propuesta de valor | Eficiencia, experiencia humana, inteligencia aplicada. |
> ...
>
> **Diseño del sistema:**
> ```
> [Frontend Web] → [API Gateway] → [Application Layer] → [Domain Layer] → [PostgreSQL]
>                        │
>                        ├─► [Auth Service]
>                        └─► [Notification Queue]
> ```
>
> **Diagrama C4 (nivel C3 – Gestión de Vacantes):**
> Describe los componentes internos del módulo y su interacción con el resto del sistema.

---

👉 **Genera ahora el entregable completo**, siguiendo la estructura anterior y asegurando que cada artefacto esté claramente documentado y conectado con la visión MVP del sistema LTI.
```
