# Propuesta de Tema: Taller de Tesis I
## Maestría en Data Mining — UBA

---

## 🎯 Pregunta de Investigación

> **¿Es posible predecir si un desarrollador adoptará y retendrá el uso de herramientas de programación asistida por IA (como GitHub Copilot) a partir de sus patrones de comportamiento en repositorios públicos previos a la adopción?**

---

## 💡 Motivación

El uso de asistentes de codificación con IA creció exponencialmente desde 2022. Sin embargo, la tasa de abandono es alta: muchos desarrolladores prueban Copilot o Cursor y lo dejan. Entender qué perfil de desarrollador adopta y retiene estas herramientas tiene valor tanto académico como práctico (para empresas como MODO que están tomando decisiones de adopción tecnológica).

---

## 📦 Dataset Principal

### GitHub Archive + GH Torrent / GHTorrent
- **URL:** https://www.gharchive.org/ y https://ghtorrent.org/
- **Qué contiene:** Eventos públicos de GitHub (commits, PRs, issues, stars, forks) desde 2011 hasta hoy
- **Volumen:** Cientos de GB, pero filtrable por fecha/usuario/lenguaje
- **Acceso fácil vía BigQuery:** Google ofrece acceso gratuito con cuota mensual

### Dataset complementario: Copilot Telemetry Study (MSR 2023)
- **Paper:** *"An Empirical Study of Deep Learning Models for Vulnerability Detection"* y estudios asociados en MSR/ICSE
- **Alternativa directa:** Dataset de Ziegler et al. (2022) — **"Productivity Assessment of Neural Code Completion"** — publicado por GitHub, contiene métricas reales de aceptación de sugerencias de Copilot
- **URL:** https://github.com/github-copilot-resources

### Dataset alternativo muy concreto: Stack Overflow Developer Survey
- **URL:** https://survey.stackoverflow.co/
- **Años disponibles:** 2017–2024 (CSV descargable)
- **Por qué sirve:** Desde 2023 incluye preguntas específicas sobre uso de IA, herramientas adoptadas, frecuencia, satisfacción y perfil del desarrollador
- **Volumen:** ~65.000–90.000 respuestas por año
- **✅ Más recomendado para empezar** — limpio, documentado, inmediatamente usable

---

## 🔬 Enfoque Concreto con Stack Overflow Survey

### Variable target (lo que querés predecir)
Crear una variable binaria:
- `1` = Desarrollador que usa IA frecuentemente y planea continuar usándola
- `0` = No usa, usa esporádicamente, o planea abandonar

### Features (variables predictoras)
- Años de experiencia, lenguajes usados, tipo de empresa
- Tamaño del equipo, rol (backend, fullstack, ML engineer…)
- Herramientas de desarrollo usadas (IDE, CI/CD, cloud)
- Nivel educativo, modalidad de trabajo (remoto/presencial)
- Satisfacción laboral, salario aproximado

---

## 🛠️ Técnicas Aplicables del Plan de Estudios

| Técnica | Aplicación en este trabajo |
|---|---|
| **Análisis exploratorio y visualización** | Perfilar tipos de adoptantes, distribuciones por país/rol/stack |
| **Preprocesamiento y feature engineering** | Encoding de variables categóricas, imputación, normalización |
| **Clasificación supervisada** | Logistic Regression, Decision Tree, Random Forest, XGBoost |
| **Evaluación de modelos** | ROC-AUC, F1, matriz de confusión, validación cruzada |
| **Selección de features** | Importancia de variables, SHAP values para interpretabilidad |
| **Clustering (complementario)** | Segmentar perfiles de desarrolladores antes de clasificar |
| **NLP básico (opcional)** | Analizar respuestas abiertas del survey ("¿por qué no usás IA?") |

---

## 📐 Estructura Sugerida del Trabajo

1. **Introducción y motivación** — adopción de IA en el desarrollo de software
2. **Estado del arte** — papers sobre Copilot, productividad, adopción tecnológica
3. **Descripción del dataset** — Stack Overflow Survey 2023 + 2024
4. **EDA** — exploración, visualización, hipótesis
5. **Modelado** — clasificación con al menos 3 algoritmos comparados
6. **Resultados e interpretación** — SHAP, qué factores predicen la adopción
7. **Conclusiones** — implicancias para empresas como MODO

---

## 🚀 Próximos Pasos Concretos

1. Descargar SO Survey 2023 y 2024 (CSV, ~50MB cada uno)
2. Identificar las columnas relevantes de IA (`AISelect`, `AIAcc`, `AISent`, etc.)
3. Definir la variable target con criterio claro
4. Hacer un EDA inicial en Python/Jupyter
5. Plantear 2–3 hipótesis para la propuesta del taller

---

## 📚 Papers de Referencia para el Marco Teórico

- Ziegler et al. (2022) — *Productivity Assessment of Neural Code Completion* (GitHub/ACM)
- Peng et al. (2023) — *The Impact of AI on Developer Productivity: Evidence from GitHub Copilot* (MIT/NBER)
- Vaithilingam et al. (2022) — *Expectation vs. Experience: Evaluating the Usability of Code Generation Tools* (CHI)
- Liang et al. (2023) — *Understanding the Usability of AI Programming Assistants* (ACM)
