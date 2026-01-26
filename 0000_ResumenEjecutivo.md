Resumen ejecutivo

Nombre del posgrado (propuesta): Posgrado en Sport Performance Data Analysis — Torso Dorado
Duración sugerida: 9 meses (part-time) o 6 meses intensivo (part-time intensivo / ejecutivo)
Formato: Híbrido (clases teóricas + laboratorios prácticos + 4 proyectos obligatorios + capstone final)
Público objetivo: Licenciados en Educación Física, Ciencias del Deporte y carreras afines con nivel básico-intermedio de Excel y ganas de aprender Python/SQL.
Modalidad de evaluación: 60% proyectos / 25% prácticas y labs / 15% quizzes y participación.

Resultados de aprendizaje (qué sabrá / podrá hacer un egresado)

Al terminar, el alumno podrá:

Diseñar pipelines de ingestión y almacenamiento de datos deportivos (CSV, APIs, webhooks) en Cloud.

Normalizar y modelar datos de sesiones para producir métricas operativas (tonnage, densidad, A:C load, RPE medio).

Construir dashboards interactivos con actualizaciones automáticas y comunicar insights a entrenadores.

Desplegar automatizaciones que actualicen métricas en tiempo real (n8n, Cloud Functions).

Implementar modelos simples de ML/heurísticos para detección de anomalías y alertas de riesgo.

Entregar un portafolio con al menos 4 proyectos operativos y un caso de estudio/Capstone.

Estructura modular (10 módulos + Capstone)

Cada módulo incluye: objetivo, unidades temáticas, labs/prácticas y entregable mínimo.

Módulo 0 — Inducción y Prerrequisitos (1 semana)

Objetivo: Homologar nivel de Python/SQL y conceptos básicos de estadística.
Contenidos: Python básico (Jupyter, pandas), SQL básico (SELECT/GROUP BY/Joins), control de versiones (Git), entorno cloud (GCP quick tour).
Entregable: Notebook + SQL query de ejemplo sobre un CSV de muestra.

Módulo 1 — Fundamentos de Datos en Deporte (3 semanas)

Objetivo: Comprender tipos de datos deportivos y su relevancia para la toma de decisión.
Temas: tipos de señales (sessions, sensors, subjective), conceptos de volumen/intensidad/tonnage, RPE, A:C load, definición de KPI.
Labs: transformar CSV de sesión en tabla normalizada; calcular tonnage por sesión.
Entregable: Documento con 8 KPIs definidos y SQL que los calcula.

Módulo 2 — Ingeniería de Datos Aplicada al Entrenamiento (4 semanas)

Objetivo: Construir pipelines reproducibles: raw → staged → curated.
Temas: Cloud Storage (buckets), BigQuery (tablas externas vs load), particionado, ingestion patterns (batch vs streaming).
Labs: subir CSV a Cloud Storage, cargar a BigQuery, crear tabla particionada, agregar ingestion desde Google Sheets vía webhook.
Entregable: Repo con scripts + README que muestra pipeline minimal (openpowerlifting → BigQuery).

Módulo 3 — Limpieza y Modelado (3 semanas)

Objetivo: Normalizar nomenclatura y construir el modelo relacional/analítico de dominio.
Temas: estándar de ejercicios (dictionary mapping), manejo de missing, imputación simple, deduplicación, SCD basics.
Labs: crear diccionario de ejercicios; transformar raw→sessions table (athlete_id, date, lift, weight_kg, reps, session_id).
Entregable: SQL/Notebook de ETL + tabla sessions lista para análisis.

Módulo 4 — Análisis Descriptivo y Series Temporales (3 semanas)

Objetivo: Extraer insights temporales (tendencias, estacionalidad, A:C load).
Temas: window functions, rolling averages, LAG/LEAD, agregaciones semanales/mensuales, detección de outliers.
Labs: queries para tonnage semanal, A:C load, %change week/week (ejemplo que ya diste).
Entregable: Notebook con queries y visualizaciones estáticas (export PDF).

Módulo 5 — Visualización y Dashboards (3 semanas)

Objetivo: Diseñar dashboards accionables para entrenadores.
Temas: principios UX para entrenadores, Looker Studio (con BigQuery), filtros, parámetros, export a PDF/HTML, embedding.
Labs: construir dashboard con filtros por atleta, lift, rango de fecha; crear visualizaciones: línea tonnage, PRs, densidad.
Entregable: Dashboard público/privado + breve video de 1 min mostrando insights (GIF o MP4).

Módulo 6 — Orquestación y Automatización (3 semanas)

Objetivo: Automatizar ingestiones y refresco de dashboards.
Temas: n8n flows, webhooks, Cloud Functions, Pub/Sub, CI/CD básico para pipelines, alerting (job-fail).
Labs: crear un flow n8n que toma un Google Sheet y actualiza BigQuery; alerta por fallo.
Entregable: Flow exportado + documentación step-by-step.

Módulo 7 — APIs y Conexiones con Apps (2 semanas)

Objetivo: Conectar datos desde apps populares y exponer métricas vía API.
Temas: Strava/TrainingPeaks API, OAuth rudiments, escribir mini-API (FastAPI) para exponer métricas.
Labs: script que consume Strava sample data y lo inserta en BigQuery; endpoint /athlete/{id}/weekly_tonnage.
Entregable: Repo con script y endpoint.

Módulo 8 — Machine Learning Básico para Deporte (opcional / 4 semanas)

Objetivo: Implementar modelos simples para alertas y predicción heurística.
Temas: feature engineering para fatiga; modelos supervisados simples; árboles, logistic regression; detección de anomalías (isolation forest); evaluación y explicación (SHAP básico).
Labs: notebook que entrena detección de anomalías sobre load time-series; alerta si A:C > threshold.
Entregable: Notebook + API de alertas o notebook reproducible.

Módulo 9 — Ética, Privacidad y Comunicación (2 semanas)

Objetivo: Protocolos de manejo de datos sensibles y comunicación efectiva con entrenadores y atletas.
Temas: anonimización, consentimiento, GDPR-like best practices, storytelling con datos, briefing para entrenadores.
Labs: redactar consentimiento, versión anonimada del caso de estudio, preparar un "one-pager" para entrenador.
Entregable: Consent form template + one-pager de findings.

Módulo 10 — Trabajo en Equipo y Gestión de Proyectos Data (2 semanas)

Objetivo: Buenas prácticas productivas: backlog, sprints, documentación, testing, monitoreo.
Temas: git flow, code review, test de pipelines, SLAs para refresh, cost awareness en cloud.
Labs: checklist de despliegue + playbook de incidentes.
Entregable: Playbook + demo de CI simple (GitHub Actions).

Capstone (8 semanas, paralelo o final)

Objetivo: Resolver un caso real desde ingestión hasta dashboard + reporte ejecutivo.
Opciones (eliges al menos 1):

Caso de estudio atleta anon.: 12 semanas de datos — intervención y posterior reporte.

Pipeline en producción: Google Form → n8n → BigQuery → Dashboard en Looker Studio + alertas.

Modelo de alerta A:C + API que notifica al entrenador.
Entregable final: Repo + Dashboard funcional + Informe ejecutivo (max 2 páginas) + video demo 3–5 min.
Evaluación: Rubrica (ver más abajo).

Mapeo de proyectos del posgrado a tu lista (encaje directo)

Proyecto 1 (MVP) = Módulos 2–5 → entregable del Módulo 2/5 (openpowerlifting → BigQuery → Dashboard).

Proyecto 2 (pipeline Google Form) = Módulos 6 + 3 + 5 → entregable n8n + Dashboard (práctica central).

Proyecto 3 (alerta A:C) = Módulos 4 + 8 → notebook y endpoint de alertas.

Proyecto 4 (caso de atleta) = Capstone.

Evaluación y ponderaciones (sugerencia)

Labs semanales / mini-entregables: 25%

Proyectos modulares (1–3): 35%

Capstone: 30%

Quizzes + participación + código limpio: 10%

Criterios Capstone (rubrica): reproducibilidad (25%), calidad del modelado/queries (25%), claridad del dashboard y storytelling (25%), impacto/insight aplicable (25%).

Herramientas, infraestructura mínima y checklist para el curso

Cuenta Google Cloud (proyectos) con BigQuery y Cloud Storage.

Looker Studio (conexión BigQuery).

n8n (self-hosted en VM o versión cloud).

Repos GitHub privados para alumnos.

Python (notebooks), pandas, requests, scikit-learn (opcional), FastAPI (opcional).

Acceso a datasets de práctica: openpowerlifting, muestras Strava (mock), CSV sintéticos.

Documentación/plantillas: diccionario de ejercicios, consent form, checklist de despliegue.

Syllabus de ejemplo (Módulo 2: Ingeniería de Datos) — semana a semana

Semana 1 — Arquitectura de pipelines (raw → staged → curated). Lab: crear bucket + upload CSV.
Semana 2 — Cargar CSV a BigQuery (tabla externa vs load). Lab: cargar CSV y particionar por date.
Semana 3 — Transformaciones SQL: crear view sessions. Lab: materialized view / scheduled query.
Semana 4 — Ingestión desde Google Sheets + webhook n8n a BigQuery. Lab: flow n8n funcionando.
Entregable módulo: Repo con scripts + demo video 3 min.

Lista de lecturas y recursos (sugeridos)

Wes McKinney — Python for Data Analysis (puntos de pandas/ETL).

BigQuery docs (Google Cloud) — guía de particionado y pricing.

Looker Studio docs / tutoriales.

Tutoriales oficiales de Strava API.

Papers / posts sobre Acute:Chronic Workload Ratio (para fundamentos).

Artículos prácticos sobre comunicación de datos (storytelling).

Nota: puedes compilar un reader pack con links y notebooks para cada módulo.

Articulación con portafolio y empleabilidad

Cada alumno sale con:

4 proyectos públicos/privados en repo + dashboards (mínimo 2 reproducibles).

Capstone presentable como caso de estudio para LinkedIn.

Micro-credential opcional en ML básico.
Posibles roles al egresar: Sport Performance Data Analyst, Analista de Rendimiento, Data Analyst en gimnasios/academias, Scientific Analyst en clubes.

Entregables mínimos por alumno (para certificar)

Repo GitHub con 3 notebooks/SQL reproducibles.

Dashboard activo (Looker Studio) con al menos 3 KPIs y filtros.

Flow de ingestión n8n o Cloud Function que actualice BigQuery automáticamente.

Capstone completo y presentable.

Recomendaciones pedagógicas y operativo del posgrado

Trabajo práctico > teoría: cada clase debe terminar con un lab que sea parte del entregable.

Mentores: 1 mentor cada 10 alumnos para code reviews y 1 sesión de feedback por proyecto.

Evaluación por pares para fomentar revisión de código y comunicación.

Plantillas (README, SQL patterns, naming conventions) para estandarizar entregables.

Plantillas de consentimiento y anonimizador de datos para prácticas con atletas reales.
