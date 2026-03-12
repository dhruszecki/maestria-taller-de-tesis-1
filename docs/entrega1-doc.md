# Taller de Tesis I — Entrega 1
## Dataset, Pregunta de Investigación y Objetivo

**Maestría en Data Mining — FCEyN, UBA**
**Grupo:** G2
**Alumno:** [Tu nombre]
**Fecha de entrega:** 5 de abril de 2025

---

## 1. Pregunta de Investigación

> **¿Qué características del perfil profesional de un desarrollador de software predicen su adopción sostenida de herramientas de programación asistida por inteligencia artificial?**

La pregunta busca identificar patrones observables —rol, experiencia, stack tecnológico, tipo de organización, nivel educativo— que distingan a los desarrolladores que incorporan activamente herramientas de IA en su flujo de trabajo de aquellos que no lo hacen o las abandonan.

---

## 2. Motivación y Relevancia

El uso de asistentes de codificación basados en IA —como GitHub Copilot, Cursor, Amazon CodeWhisperer o Claude— creció de manera exponencial a partir de 2022. Sin embargo, la adopción no es homogénea: distintos estudios señalan que una fracción significativa de desarrolladores que prueban estas herramientas no las retiene en su práctica cotidiana (Ziegler et al., 2022; Peng et al., 2023).

Comprender qué perfil de desarrollador adopta y sostiene el uso de IA tiene relevancia directa para:

- **Empresas de tecnología** que deben tomar decisiones de adopción y capacitación (como el contexto de [nombre de tu empresa]).
- **Equipos de ingeniería** que evalúan el retorno de inversión de licencias de herramientas de IA.
- **La academia**, donde la predicción de adopción tecnológica en contextos de desarrollo de software es un área activa de investigación.

---

## 3. Dataset

### 3.1 Fuente

**Stack Overflow Developer Survey 2023 y 2024**
- URL: [https://survey.stackoverflow.co/](https://survey.stackoverflow.co/)
- Licencia: Open Database License (ODbL) — uso libre con atribución
- Formato: CSV descargable públicamente

### 3.2 Descripción General

Stack Overflow realiza anualmente una encuesta masiva a desarrolladores de todo el mundo. A partir de 2023 incorporó un bloque específico de preguntas sobre adopción, actitud y experiencia con herramientas de IA, lo que hace a este dataset especialmente adecuado para la pregunta de investigación.

| Atributo | 2023 | 2024 |
|---|---|---|
| Respuestas | ~89.000 | ~65.000 |
| Columnas | ~84 | ~90 |
| Cobertura geográfica | +180 países | +180 países |
| Bloque de IA incluido | ✅ | ✅ |

### 3.3 Variables Clave

**Variables de IA (para construir el target):**

| Columna | Descripción |
|---|---|
| `AISelect` | ¿Usás herramientas de IA en tu trabajo actualmente? |
| `AIAcc` | ¿Cuál es tu actitud hacia la IA en el desarrollo? |
| `AISent` | ¿Cómo te sentís respecto al futuro de la IA? |
| `AIBen` | ¿Creés que la IA te beneficia en tu trabajo? |
| `AIToolCurrently` | ¿Qué herramientas de IA usás actualmente? |

**Variables de perfil (features predictoras):**

| Columna | Descripción |
|---|---|
| `DevType` | Rol del desarrollador (backend, fullstack, ML, etc.) |
| `YearsCodePro` | Años de experiencia profesional programando |
| `OrgSize` | Tamaño de la organización |
| `Country` | País de residencia |
| `EdLevel` | Nivel educativo alcanzado |
| `Employment` | Modalidad de empleo |
| `LanguageHaveWorkedWith` | Lenguajes de programación utilizados |
| `CompTotal` | Compensación total anual |
| `WorkExp` | Años de experiencia laboral total |

### 3.4 Justificación de la Elección del Dataset

Se eligió el Stack Overflow Developer Survey por las siguientes razones:

1. **Disponibilidad inmediata**: CSV público, sin barreras de acceso ni aprobación institucional.
2. **Cobertura y tamaño**: más de 150.000 respuestas combinadas entre 2023 y 2024, con representación global.
3. **Relevancia temática**: es el único dataset público masivo que incluye preguntas específicas sobre adopción y actitud hacia herramientas de IA en el contexto del desarrollo de software.
4. **Reproductibilidad**: al ser público y con licencia abierta, cualquier revisión del trabajo puede replicar los resultados exactos.

---

## 4. Variable Target

Se construye una variable binaria que representa la **adopción sostenida de IA**:

```
target = 1  →  El desarrollador usa IA actualmente en su trabajo
               Y tiene una actitud favorable o muy favorable hacia ella

target = 0  →  Cualquier otro caso (no usa, actitud negativa o neutral)
```

**Justificación del criterio:** La combinación de uso activo + actitud positiva captura la noción de "adoptante sostenido", diferenciándola de quienes probaron la herramienta pero la abandonaron, o de quienes la usan de forma reluctante. Este criterio está respaldado por el modelo TAM (Technology Acceptance Model), ampliamente usado en estudios de adopción tecnológica.

**Distribución esperada:** [completar con el valor real obtenido del código]
- Target = 1 (adoptantes): XX.XXX respuestas (XX%)
- Target = 0 (no adoptantes): XX.XXX respuestas (XX%)

---

## 5. Objetivo General

Desarrollar un modelo de clasificación supervisada capaz de predecir si un desarrollador de software adoptará de manera sostenida herramientas de programación asistida por IA, a partir de características observables de su perfil profesional.

---

## 6. Objetivos Específicos

1. Realizar un análisis exploratorio del dataset para identificar patrones de adopción según perfil demográfico, experiencia y stack tecnológico.
2. Construir y validar una variable target binaria que represente la adopción sostenida de herramientas de IA.
3. Aplicar técnicas de segmentación no supervisada (clustering) para identificar perfiles naturales de desarrolladores.
4. Entrenar y comparar al menos tres modelos de clasificación supervisada (Regresión Logística, Random Forest, XGBoost).
5. Interpretar los resultados mediante técnicas de explicabilidad (SHAP values) para identificar los factores más predictivos.

---

## 7. Limitaciones Conocidas

| Limitación | Impacto | Mitigación |
|---|---|---|
| **Sesgo de autoselección** | Los encuestados son usuarios activos de Stack Overflow, no representan a todos los devs del mundo | Aclarar en el alcance del trabajo |
| **Datos de encuesta** (self-reported) | Las respuestas pueden no reflejar comportamiento real | Combinar con columnas de actitud como validación cruzada |
| **Variables faltantes** | Columnas como `CompTotal` tienen alta tasa de NaN | Imputación o exclusión justificada en la Entrega 2 |
| **Cambio de nomenclatura entre años** | Algunas columnas cambian de nombre entre 2023 y 2024 | Alineación manual documentada en el código |
| **Corte temporal** | Los datos llegan hasta 2024; el mercado de IA evoluciona rápido | Aclarar que las conclusiones aplican a ese período |

---

## 8. Metodología Prevista (resumen)

El trabajo seguirá el siguiente pipeline, que se detallará en la Entrega 2:

1. **Preprocesamiento** — limpieza, encoding, alineación entre años, construcción del target
2. **AED** — análisis exploratorio con visualizaciones
3. **Clustering** — segmentación no supervisada de perfiles (K-Means)
4. **Clasificación** — modelos supervisados comparados con validación cruzada
5. **Interpretabilidad** — SHAP values para explicar las predicciones

---

## 9. Referencias

- Ziegler, A. et al. (2022). *Productivity Assessment of Neural Code Completion*. ACM MAPS.
- Peng, S. et al. (2023). *The Impact of AI on Developer Productivity: Evidence from GitHub Copilot*. MIT/NBER Working Paper.
- Vaithilingam, P. et al. (2022). *Expectation vs. Experience: Evaluating the Usability of Code Generation Tools*. CHI 2022.
- Liang, J. et al. (2023). *Understanding the Usability of AI Programming Assistants*. ACM.
- Davis, F. D. (1989). *Perceived Usefulness, Perceived Ease of Use, and User Acceptance of Information Technology*. MIS Quarterly. *(TAM)*

---

*Documento preparado para Taller de Tesis I — FCEyN UBA*
