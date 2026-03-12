# 🤖 Predicción de Adopción de IA en Desarrolladores

**Taller de Tesis I — Maestría en Data Mining, FCEyN UBA**
**Alumno:** [Tu nombre] · **Grupo:** G2

---

## 📋 Pregunta de Investigación

> ¿Qué características del perfil profesional de un desarrollador de software predicen su adopción sostenida de herramientas de programación asistida por inteligencia artificial?

---

## 📦 Dataset

**Stack Overflow Developer Survey 2023 + 2024**
- Fuente: https://survey.stackoverflow.co/
- Licencia: Open Database License (ODbL)
- Los archivos CSV **no están incluidos en este repositorio** (ver instrucciones abajo)

---

## 🚀 Setup

### Prerequisitos
- Python 3.11+
- [uv](https://docs.astral.sh/uv/) instalado

### Instalación

```bash
# Clonar el repositorio
git clone https://github.com/[tu-usuario]/tesis-ia-devs.git
cd tesis-ia-devs

# Instalar dependencias
uv sync
```

### Datos

1. Descargar los CSVs desde https://survey.stackoverflow.co/
2. Crear la carpeta `data/` en la raíz del proyecto
3. Colocar los archivos con estos nombres exactos:

```
data/
├── survey_results_public_2023.csv
└── survey_results_public_2024.csv
```

### Abrir en VS Code

```bash
code .
```

Instalar la extensión **Jupyter** de Microsoft si no la tenés.
VS Code detecta el entorno `uv` automáticamente.

---

## 📁 Estructura del Proyecto

```
tesis-ia-devs/
│
├── data/                         # ← NO incluido en git
│   ├── survey_results_public_2023.csv
│   └── survey_results_public_2024.csv
│
├── notebooks/
│   ├── 01_exploracion.ipynb         # Entrega 1 — Dataset, pregunta y objetivo
│   ├── 02_preprocesamiento_eda.ipynb # Entrega 2 — Metodología y AED
│   ├── 03_clustering.ipynb          # Entrega 3 — Segmentación no supervisada
│   └── 04_modelado.ipynb            # Entrega 3/4 — Clasificación + SHAP
│
├── outputs/                      # Gráficos exportados (PNG)
│   └── .gitkeep
│
├── docs/                         # Documentos de entrega (PDF/DOCX)
│   ├── entrega1_dataset_pregunta_objetivo.md
│   ├── entrega2_metodologia_aed.md
│   ├── entrega3_introduccion_resultados.md
│   └── entrega4_discusion_conclusiones.md
│
├── .gitignore
├── pyproject.toml                # Dependencias (uv)
└── README.md
```

---

## 🗓️ Cronograma de Entregas (G2)

| # | Tema | Clase | Deadline |
|---|------|-------|----------|
| 1 | Dataset, pregunta y objetivo | 26/3 | **5/4** |
| 2 | Metodología y AED | 30/4 | **10/5** |
| 3 | Introducción y resultados | 28/5 | **7/6** |
| 4 | Discusión y conclusiones | 25/6 | **5/7** |

---

## 🛠️ Stack Tecnológico

| Herramienta | Uso |
|---|---|
| `pandas` | Manipulación del dataset |
| `numpy` | Operaciones numéricas |
| `matplotlib` + `seaborn` | Visualizaciones |
| `scikit-learn` | Preprocesamiento, clustering, clasificación |
| `xgboost` | Modelo de clasificación avanzado |
| `shap` | Interpretabilidad de modelos |
| `jupyterlab` | Entorno de notebooks |

---

## 🔬 Pipeline del Trabajo

```
SO Survey CSV  →  Preprocesamiento  →  AED  →  Clustering  →  Clasificación  →  SHAP
   2023 + 2024       (limpieza,          (EDA,    (K-Means,      (LR, RF,         (interpretación
                      encoding,           viz)     perfiles)      XGBoost)          de resultados)
                      target)
```

---

## 📚 Referencias Principales

- Ziegler et al. (2022). *Productivity Assessment of Neural Code Completion*. ACM.
- Peng et al. (2023). *The Impact of AI on Developer Productivity*. MIT/NBER.
- Vaithilingam et al. (2022). *Expectation vs. Experience*. CHI 2022.
- Liang et al. (2023). *Understanding the Usability of AI Programming Assistants*. ACM.

---

## .gitignore recomendado

```
# Datos (pesados, no van al repo)
data/

# Entorno Python
.venv/
__pycache__/
*.pyc
.ipynb_checkpoints/

# OS
.DS_Store
Thumbs.db

# Outputs grandes
outputs/*.png
```