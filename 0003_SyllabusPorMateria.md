Syllabus detallado por materia

Para facilitar lectura, cada materia muestra: duración (semanas / h aprox.), objetivo, semana a semana, bibliografía por semana, lab(s) y entregable.

M1 — Fisiología del Esfuerzo Aplicada al Análisis de Datos

Duración: 3 semanas (30 h)
Objetivo: Dar la base fisiológica que sustenta las métricas de entrenamiento; habilitar a traducir fenómenos biológicos a features medibles.

Semana 1 — Sistemas energéticos y demandas

Contenido: ATP-PC, glucolítico, oxidativo; tipos de esfuerzo (explosivo, submáximo, resistencia).

Bibliografía: capítulo sobre sistemas energéticos en Exercise Physiology (McArdle). Artículo corto sobre interpretación de datos externos vs internos.

Lab: Dataset sintético con sesiones (duración, intensidad, repeticiones). Heurística: asignar “dominancia energética” por sesión (reglas basadas en duración e intensidad).

Entregable: Notebook con heurística aplicada y visualización simple.

Semana 2 — Fatiga, recuperación y adaptación

Contenido: fatiga central/periférica, supercompensación, tiempos de recuperación, indicadores de sobrecarga.

Bibliografía: Bompa (cap. sobre recuperación), artículo sobre A:C load.

Lab: Calcular rolling averages (7/28 días) y visualizar tendencias. Implementar una métrica simple de “fatiga acumulada”.

Entregable: Notebook + explicación de 2 decisiones de entrenamiento derivados.

Semana 3 — Carga interna vs externa y RPE

Contenido: comparación carga externa (tonnage, distancia) vs interna (RPE, HR), valor práctico del RPE.

Bibliografía: paper sobre correlación RPE vs carga externa (se aporta PDF).

Lab: Dataset con tonnage y RPE → correlación y scatter plot; detectar sesiones con alto RPE y bajo volumen (bandera).

Entregable: Notebook + 1 insight accionable.

M2 — Periodización del Entrenamiento para Analistas

Duración: 4 semanas (36 h)
Objetivo: Traducir modelos de periodización a estructuras de datos y KPIs de seguimiento.

Semana 1 — Modelos de periodización (visión)

Contenido: lineal, ondulante, bloques; cuándo usar cada uno.

Bibliografía: Bompa (sección periodización), artículos comparativos.

Lab: Representar gráficamente (mock) la carga esperada de un mesociclo.

Semana 2 — Macro / Meso / Microciclos como datos

Contenido: etiquetas temporales, tagging de sesiones.

Bibliografía: capítulos selectos sobre mesociclos.

Lab: crear tabla training_blocks y unir con sessions (SQL).

SQL ejemplo:

-- Crear tabla blocks (ejemplo conceptual)
CREATE OR REPLACE TABLE dataset.training_blocks AS
SELECT
  block_id,
  athlete_id,
  DATE(start_date) AS start_date,
  DATE(end_date) AS end_date,
  block_type -- 'strength', 'hypertrophy', 'taper'
FROM UNNEST([
  STRUCT('b1' AS block_id, 'ath1' AS athlete_id, '2025-01-01', '2025-01-21', 'strength')
]);

Semana 3 — Gestión de carga y riesgo

Contenido: A:C Load, ramp rates, señales de alarma.

Bibliografía: artículos críticos sobre A:C Load.

Lab: SQL para calcular A:C load (ver sección Queries).

Entregable: Dashboard microciclo vs plan.

Semana 4 — Ajustes y feedback

Contenido: cómo traducir desviaciones a decisiones (deload, ajuste de intensidad).

Lab: Simulación de dataset con imprevistos y plan de intervención.

Entregable: Informe corto con 3 recomendaciónes.

M3 — Introducción al Análisis de Datos Deportivos

Duración: 2 semanas (24 h)
Objetivo: Fundamentos prácticos de análisis, métricas y estadística descriptiva.

Semana 1 — Tipos de datos y KPIs

Contenido: tipos de señales (sesiones, sensores, subjetivos), definición de KPIs clave.

Bibliografía: Wes McKinney (cap. intro) y guías prácticas.

Lab: cargar CSV a pandas, explorar y describir.

Semana 2 — Estadística descriptiva aplicada

Contenido: media, mediana, desviación, percentiles, outliers.

Lab: notebook con EDA (exploratory data analysis) y un mini-report.

Entregable: Notebook + readme.

M4 — Ingeniería de Datos para el Rendimiento Deportivo

Duración: 6 semanas (48 h)
Objetivo: Construir pipelines reproducibles en Cloud (raw → staged → curated).

Semana 1 — Arquitectura de pipelines

Contenido: patrones ETL/ELT, considerations for cloud costs.

Bibliografía: BigQuery docs (particionado), artículos sobre data lake vs warehouse.

Lab: diseñar arquitectura simple.

Semana 2 — Cloud Storage y buckets

Contenido: buckets, ciclos de vida, versioning, seguridad básica.

Lab: crear bucket y subir CSV.

Semana 3 — BigQuery: tablas externas y cargas

Contenido: external tables vs load jobs, particionado, clustering.

Lab: cargar CSV a BigQuery y crear tabla particionada.

SQL ejemplo (crear tabla a partir de CSV cargado):

CREATE OR REPLACE TABLE `proyecto.dataset.openpl_raw`
PARTITION BY DATE(timestamp)
AS SELECT * FROM `proyecto.bucket.openpl_csv`;

Semana 4 — Scheduling y materialized views

Contenido: scheduled queries, materialized views, costos.

Lab: crear scheduled query para transformar raw → staged.

Semana 5 — Data quality y testing

Contenido: checks, row counts, schema drift detection.

Lab: implementar tests básicos (assert row counts, null checks).

Semana 6 — Deploy y documentación

Entregable: pipeline reproducible (scripts + README + diagrama).

M5 — Modelado y Limpieza de Datos de Entrenamiento

Duración: 4 semanas (36 h)
Objetivo: Estandarizar nomenclaturas, imputar y modelar table sessions.

Semana 1 — Diccionario de ejercicios y mapping

Contenido: técnicas para normalizar strings (fuzzy matching).

Lab: notebook con funciones de mapping (pandas + fuzzywuzzy).

Snippet Python:

from rapidfuzz import process
candidates = ["back squat", "back-squat", "sentadilla trasera"]
match = process.extractOne("backs quat", candidates)

Semana 2 — Manejo de missing y deduplicación

Lab: estrategias de imputación simples y dedupe.

Semana 3 — Transformaciones y SCD basics

Contenido: Slowly changing dimensions para atletas y equipos.

Lab: crear tablas dimension y hechos (star schema).

Semana 4 — Materialized views y performance

Entregable: tabla sessions + documentación mapping.

SQL ejemplo (crear sessions agregada):

CREATE OR REPLACE TABLE `proyecto.dataset.sessions` AS
SELECT
  athlete_id,
  session_id,
  DATE(timestamp) AS session_date,
  lift,
  SUM(weight_kg * reps) AS tonnage,
  SUM(reps) AS total_reps,
  AVG(rpe) AS avg_rpe,
  APPROX_COUNT_DISTINCT(exercise_id) AS distinct_exercises
FROM `proyecto.dataset.openpl_raw`
GROUP BY athlete_id, session_id, session_date, lift;

M6 — Análisis de Rendimiento y Series Temporales

Duración: 5 semanas (40 h)
Objetivo: Aplicar técnicas temporales para medir evolución, tendencias y señales de alarma.

Semana 1 — Window functions y rolling

Lab: SQL con window functions (LAG, LEAD, AVG over window).

SQL: tonnage semanal y % cambio (ya incluido, repetir con safe_divide).
(Usar el SQL que diste antes — se puede reutilizar.)

Semana 2 — Acute:Chronic Load (A:C)

Contenido: cálculo A:C (exponencial vs simple moving averages).

Lab: implementar A:C (14d vs 28d) y visualización.

SQL ejemplo A:C (simple):

WITH daily AS (
  SELECT athlete_id, DATE(session_date) AS day, SUM(tonnage) AS daily_tonnage
  FROM `proyecto.dataset.sessions`
  GROUP BY athlete_id, day
)
SELECT
  athlete_id,
  day,
  daily_tonnage,
  AVG(daily_tonnage) OVER (PARTITION BY athlete_id ORDER BY day ROWS BETWEEN 13 PRECEDING AND CURRENT ROW) AS acute_14d,
  AVG(daily_tonnage) OVER (PARTITION BY athlete_id ORDER BY day ROWS BETWEEN 27 PRECEDING AND CURRENT ROW) AS chronic_28d
FROM daily;

Semana 3 — Detección de outliers y anomalías

Lab: isolation forest en notebook (scikit-learn) o heurística.

Semana 4 — Correlaciones RPE vs rendimiento

Lab: correlaciones, cross-correlation time-lag.

Python snippet:

df.groupby('athlete_id').apply(lambda g: g['tonnage'].corr(g['rpe']))

Semana 5 — Resumen y entrega

Entregable: Notebook con 3 análisis temporales por atleta y una recomendación.

M7 — Visualización de Datos y Dashboards para Entrenadores

Duración: 4 semanas (36 h)
Objetivo: Diseñar dashboards accionables y exportables.

Semana 1 — Principios UX para entrenadores

Contenido: jerarquía de información, reducir ruido.

Lab: wireframe en Figma/PowerPoint.

Semana 2 — Looker Studio: conexión BigQuery

Lab: crear report con filtros, parámetros y control de acceso.

Semana 3 — Visualizaciones avanzadas

Contenido: small multiples, sparkline, tablas con heatmaps.

Lab: implementar gráficos: tonnage semanal, PR timeline, density chart.

Semana 4 — Export y storytelling

Entregable: Dashboard + video demo 2 min (narrativa: problema → insight → acción).

M8 — Automatización y Orquestación de Flujos de Datos

Duración: 4 semanas (36 h)
Objetivo: Automatizar pipelines y refresco de dashboards, implementar alertas.

Semana 1 — Introducción a n8n / Cloud Functions

Lab: crear flow simple en n8n que toma Google Sheet → BigQuery.

Semana 2 — Webhooks y seguridad

Contenido: validación payloads, rate limits.

Lab: proteger webhooks con tokens y validate payloads.

Semana 3 — Alerting y observability

Contenido: job-fail alerting, logs, retries.

Lab: configurar alertas por email/slack (simulado).

Semana 4 — Despliegue y documentación

Entregable: Flow exportado + playbook.

n8n flow steps (concepto):

Webhook receive (Google Form webhook)

Transform node (map fields)

HTTP Request / BigQuery insert node

Success/Fail handler -> notify slack/email

M9 — Integración con Apps y APIs Deportivas

Duración: 3 semanas (28 h)
Objetivo: Conectar APIs de terceros y exponer métricas.

Semana 1 — OAuth & API basics

Lab: consumir API pública (strava sample) y parsear JSON.

Python snippet (requests):

import requests
resp = requests.get("https://www.strava.com/api/v3/athlete/activities", headers={"Authorization": f"Bearer {TOKEN}"})
data = resp.json()

Semana 2 — Transformar y cargar

Lab: script que normaliza y sube a BigQuery.

Semana 3 — Exponer métricas con FastAPI

Lab: mini-API /athlete/{id}/weekly_tonnage

FastAPI snippet:

from fastapi import FastAPI
app = FastAPI()
@app.get("/athlete/{athlete_id}/weekly_tonnage")
def weekly(athlete_id: str):
    # query BigQuery client here and return JSON
    return {"athlete_id": athlete_id, "data": []}


Entregable: Repo con script + endpoint funcional (local/mock).

M10 — Introducción al Machine Learning Aplicado al Deporte (Optativa)

Duración: 5 semanas (40 h)
Objetivo: Modelos simples para detección de anomalías y predicción heurística.

Semana 1 — Feature engineering para series temporales

Lab: crear features rolling (mean, std, slope).

Semana 2 — Modelos supervisados básicos

Lab: regresión simple para predecir tonnage next week.

Semana 3 — Detección de anomalías

Lab: IsolationForest / LocalOutlierFactor para sesiones atípicas.

Semana 4 — Evaluación y explainability

Lab: precision/recall, SHAP básico para árboles.

Semana 5 — Deploy (opcional)

Entregable: Notebook con modelo + endpoint o alerta.

M11 — Ética, Privacidad y Comunicación de Datos Deportivos

Duración: 3 semanas (28 h)
Objetivo: Protocolos de consentimiento, anonimización y comunicación responsable.

Semana 1 — Legislación y consentimiento

Lab: redactar consent form.

Semana 2 — Anonimización y minimización

Lab: pipeline para anonimizar dataset (hash IDs, remove PHI).

Semana 3 — Comunicación de insights

Lab: one-pager profesional para entrenador + demo de presentación.

Entregable: Templates y one-pager.

M12 — Trabajo Final Integrador (Capstone)

Duración: 8–12 semanas (80 h) — ver guía detallada después.
Objetivo: Proyecto final integral (ver sección Capstone abajo).

Queries y snippets clave (colección para labs y entregables)

Tonaje por sesión (BigQuery) — ya mostrado antes; versión compacta:

SELECT
  session_id,
  athlete_id,
  DATE(timestamp) AS session_date,
  lift,
  SUM(weight_kg * reps) AS tonnage,
  SUM(reps) AS total_reps
FROM `proyecto.dataset.openpl_raw`
GROUP BY session_id, athlete_id, session_date, lift
ORDER BY session_date DESC;


Totales semanales con % cambio (BigQuery)

WITH weekly AS (
  SELECT
    athlete_id,
    DATE_TRUNC(DATE(timestamp), WEEK(MONDAY)) AS week_start,
    SUM(weight_kg * reps) AS total_tonnage
  FROM `proyecto.dataset.openpl_raw`
  GROUP BY athlete_id, week_start
)
SELECT
  w.*,
  LAG(total_tonnage) OVER (PARTITION BY athlete_id ORDER BY week_start) AS prev_tonnage,
  SAFE_DIVIDE(total_tonnage - LAG(total_tonnage) OVER (PARTITION BY athlete_id ORDER BY week_start),
              LAG(total_tonnage) OVER (PARTITION BY athlete_id ORDER BY week_start)) * 100 AS pct_change
FROM weekly w
ORDER BY athlete_id, week_start DESC;


A:C Load (14/28 días)

WITH daily AS (
  SELECT athlete_id, DATE(session_date) AS day, SUM(tonnage) AS daily_tonnage
  FROM `proyecto.dataset.sessions`
  GROUP BY athlete_id, day
)
SELECT
  athlete_id,
  day,
  AVG(daily_tonnage) OVER (PARTITION BY athlete_id ORDER BY day ROWS BETWEEN 13 PRECEDING AND CURRENT ROW) AS acute_14d,
  AVG(daily_tonnage) OVER (PARTITION BY athlete_id ORDER BY day ROWS BETWEEN 27 PRECEDING AND CURRENT ROW) AS chronic_28d,
  SAFE_DIVIDE(
    AVG(daily_tonnage) OVER (PARTITION BY athlete_id ORDER BY day ROWS BETWEEN 13 PRECEDING AND CURRENT ROW),
    AVG(daily_tonnage) OVER (PARTITION BY athlete_id ORDER BY day ROWS BETWEEN 27 PRECEDING AND CURRENT ROW)
  ) AS ac_ratio
FROM daily;


PRs por atleta (máximo weight x reps)

SELECT
  athlete_id,
  lift,
  MAX(weight_kg) AS pr_weight,
  ANY_VALUE(session_date) KEEP (DENSE_RANK FIRST ORDER BY weight_kg DESC) AS pr_date
FROM `proyecto.dataset.sessions`
GROUP BY athlete_id, lift;


(Nota: BigQuery no tiene KEEP — alternativa usar window rank).

Densidad: tonnage / tiempo (mins)

SELECT
  session_id,
  athlete_id,
  SUM(weight_kg * reps) / SUM(duration_minutes) AS density
FROM `proyecto.dataset.sessions`
GROUP BY session_id, athlete_id;


RPE vs tonnage correlación (pandas)

import pandas as pd
df = pd.read_gbq("SELECT athlete_id, tonnage, avg_rpe FROM proyecto.dataset.sessions")
df.groupby('athlete_id').apply(lambda g: g['tonnage'].corr(g['avg_rpe']))

Guía para implementar el Capstone (detallada)

Propósito: que cada alumno entregue un proyecto reproducible que demuestre dominio técnico, interpretación fisiológica y comunicación profesional.

Casos posibles (elige 1 por equipo/alumno)

Pipeline en producción (MVP operativo)

Google Form → n8n → BigQuery → Looker Studio dashboard con alertas.

Entrega: repo, flow exportado, dashboard, video demo.

Caso de estudio atleta (anónimo)

12 semanas de datos (real o simulada): diagnóstico, intervención, resultados.

Entrega: notebook + dashboard + informe de intervención.

Sistema de alertas A:C + endpoint

Modelo heurístico/ML que detecta riesgo y expone alertas via API.

Entrega: notebook, endpoint (FastAPI), demo.

Integración multi-source

Juntar datos de Strava + sesión manual + HR + RPE → análisis combinado.

Entrega: repo, ETL, dashboard y one-pager.

Proyecto libre validado

Propuesta deberá aprobarse por mentor (alineada a objetivos del posgrado).

Cronograma sugerido (8–12 semanas)

Semana 0 (Kickoff): Definición de alcance, dataset y mentor asignado. (entregable: Project brief 1 página)

Semana 1–2 (Ingesta & modelado): Pipeline mínimo funcionando (raw → sessions). (entregable: script + sample load)

Semana 3–4 (Análisis exploratorio): EDA, KPIs definidos, primeras visualizaciones. (entregable: notebook EDA)

Semana 5–6 (Dashboards & Automations): Dashboard funcional + flow de refresh. (entregable: dashboard + flow)

Semana 7 (Refinado & ML opcional): Modelos/alertas y tests. (entregable: notebook modelo)

Semana 8 (Entrega final): Repo, dashboard, informe ejecutivo y video demo. Defensa frente a jurado.

Si se asignan 12 semanas, incluir 2 semanas buffer para data cleaning y refinamiento.

Hitos obligatorios y plantillas (descargables conceptuales)

Project Brief (1 página)

Título, objetivo, dataset, métricas clave, entregables, timeline.

README del repo

Estructura de carpetas, cómo reproducir (creds necesitan variables), comandos principales.

Data Dictionary

Columnas, tipos, definiciones y posibles valores (exercise_map).

Informe ejecutivo (máx 2 páginas)

Problema, approach, 3 insights accionables, recomendación concreta.

Dashboard checklist

KPIs visibles, filtros por atleta/fechas, exportable, control de acceso.

Consent form template (si se usan datos reales)

Incluye propósito, uso, anonimizacion, duración de almacenamiento.

Playbook de despliegue

Cómo refrescar pipeline, rollback, runs fallidas.

Rúbrica de evaluación (detallada)

Total 100 puntos — dividida en criterios técnicos, científicos y comunicacionales.

A. Reproducibilidad y calidad técnica (25 pts)

0–5: Repo sin instrucciones.

6–12: Scripts funcionan localmente, pero faltan pasos.

13–18: Pipeline reproducible con README claro.

19–25: Pipeline reproducible, tests básicos, CI simple o script de deploy.

B. Modelado de datos y queries (20 pts)

0–5: Datos sin normalizar.

6–12: Modelado básico, algunas inconsistencias.

13–16: Buen modelado, tablas bien documentadas.

17–20: Modelo optimizado, particionado/cluster y materialized views cuando aplica.

C. Fundamento fisiológico / periodización (20 pts)

0–5: No vincula resultados con fisiología.

6–12: Menciones superficiales.

13–16: Insights respaldados por teoría de entrenamiento.

17–20: Justificación sólida, decisiones de entrenamiento claras y válidas.

D. Visualización & storytelling (20 pts)

0–5: Dashboard confuso o inexistente.

6–12: Visuales funcionales pero no priorizan.

13–16: Buen dashboard, filtros y narrativa clara.

17–20: Excelente storytelling, exportable y fácil de interpretar por entrenador.

E. Impacto y aplicabilidad (10 pts)

0–3: Escasa aplicabilidad.

4–7: Aplicable en contexto reducido.

8–10: Alto impacto, escalable o replicable.

F. Presentación y defensa (5 pts)

Claridad, respuestas en Q&A, capacidad de defender supuestos.

Notas de corrección: cada criterio incluye comentarios detallados por el jurado; las fallas críticas (p. ej. uso indebido de datos personales sin consentimiento) anulan/aplican penalidades severas.

Ejemplo de checklist mínimo para entregar (Capstone)

 README con pasos de reproducción.

 Dataset (o link y script que descargue los datos).

 Notebook EDA + SQL principales.

 Dashboard con filtros y KPIs.

 Script / flow que actualiza BigQuery.

 Informe ejecutivo (2 págs) + video demo.

 Consentimiento/anonimización (si aplica).

Templates (texto modelo resumido — copia/pega y adapta)
Project Brief (modelo)
Título:
Equipo/alumno:
Objetivo:
Dataset (fuente / tamaño / privacidad):
Métricas clave:
Entregables:
Timeline (8 semanas):
Riesgos/mitigaciones:
Mentor:

README (estructura recomendada)
/README.md
/docs/
  - data_dictionary.md
  - playbook.md
/notebooks/
  - 01_ingest.ipynb
  - 02_eda.ipynb
  - 03_analysis.ipynb
/scripts/
  - ingest.py
  - deploy_flow.sh
/dashboard/
  - lookerstudio_link.txt

Informe ejecutivo (estructura)

Contexto y objetivo (1–2 frases)

Qué medimos y por qué (KPIs)

3 insights clave (cada uno con evidencia visual y métrica)

Recomendaciones concretas (acciones del entrenador)

Riesgos y limitaciones

Recursos adicionales y deliverables docentes

Rubricas en formato Excel/Google Sheets (para que el jurado marque los puntajes).

Checklist de revisión por pares (2 alumnos revisan otro capstone).

Guía rápida de entrega (cómo publicar dashboard y permisos).

Últimos consejos pedagógicos para el capstone

Forzar un Project Brief 1 semana después del kickoff: evita scope creep.

Mentor con revisiones semanales de 20–30 min.

Revisión por pares obligatoria para fomentar feedback temprano.

Entrega intermedia (MVP) en la semana 4 con criterio mínimo: pipeline + 2 KPIs.
