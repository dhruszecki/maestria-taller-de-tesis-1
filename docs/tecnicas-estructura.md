# Técnicas Aplicables → Estructura del Trabajo
## Cómo cada materia se traduce en una sección concreta

---

## SECCIÓN 1 — Introducción y Pregunta de Investigación
> *No requiere técnica específica, pero define todo lo demás*

**Qué va acá:**
- Contexto: explosión del uso de IA en desarrollo de software (2022–2024)
- Problema: alta tasa de abandono, adopción desigual entre perfiles
- Pregunta: ¿Qué características predicen que un dev adopte y retenga herramientas de IA?
- Justificación de por qué es relevante para una empresa como MODO

---

## SECCIÓN 2 — Dataset y Preprocesamiento
> *Fundamento: Análisis Exploratorio / Estadística*

**Qué vas a hacer:**
- Cargar SO Survey 2023 + 2024 con `pandas`
- Identificar columnas clave de IA: `AISelect`, `AIAcc`, `AISent`, `AIBen`, `AIToolCurrently`
- Construir la **variable target binaria**:
  - `1` = usa IA frecuentemente + actitud positiva (`AIAcc` = "Favorable" o "Very favorable")
  - `0` = no usa, o usa pero con actitud negativa/neutral
- Tratar valores faltantes (imputación o descarte justificado)
- Encoding de categóricas (`OrdinalEncoder`, `OneHotEncoder`)
- Normalización de numéricas si el modelo lo requiere

**Por qué justifica la materia:**
Estadística descriptiva, análisis de distribuciones, detección de outliers, correlaciones → todo es contenido directo de Análisis Exploratorio.

---

## SECCIÓN 3 — EDA (Análisis Exploratorio)
> *Fundamento: Análisis Exploratorio / Estadística*

**Preguntas que vas a responder con visualizaciones:**
- ¿Qué porcentaje adopta IA? ¿Varía por país, rol, años de experiencia?
- ¿Los devs que usan más lenguajes modernos (TypeScript, Rust, Go) adoptan más?
- ¿Hay diferencia entre empresas chicas vs grandes?
- ¿Correlación entre salario y adopción de IA?

**Visualizaciones concretas:**
```python
# Distribución de adopción por rol
sns.countplot(data=df, x='DevType', hue='target')

# Heatmap de correlaciones
sns.heatmap(df[numeric_cols].corr(), annot=True)

# Adopción por años de experiencia
df.groupby('YearsCodePro')['target'].mean().plot(kind='bar')
```

**Output esperado:** 6–8 visualizaciones con interpretación, 2–3 hipótesis que guíen el modelado.

---

## SECCIÓN 4 — Segmentación de Perfiles (Clustering)
> *Fundamento: Aprendizaje No Supervisado*

**Por qué incluirlo antes del modelo supervisado:**
En lugar de meter todos los devs en un solo clasificador, primero segmentás perfiles naturales. Esto enriquece el análisis y justifica la materia de No Supervisado.

**Qué vas a hacer:**
- Aplicar **K-Means** sobre variables de perfil (rol, stack, experiencia, empresa)
- Determinar k óptimo con el método del codo + Silhouette Score
- Caracterizar cada cluster: *"Cluster 2 = devs senior de empresas grandes, alta adopción de IA"*
- Usar el cluster como feature adicional en el modelo supervisado

```python
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X_profile)

kmeans = KMeans(n_clusters=4, random_state=42)
df['cluster'] = kmeans.fit_predict(X_scaled)
```

**Output esperado:** 3–5 clusters interpretables con nombres descriptivos y tasa de adopción de IA por cluster.

---

## SECCIÓN 5 — Modelado Predictivo
> *Fundamento: Aprendizaje Supervisado*

**Objetivo:** Predecir la variable target (adopta/no adopta IA) con al menos 3 modelos comparados.

### Modelos a usar (de menor a mayor complejidad):

| Modelo | Por qué incluirlo |
|---|---|
| **Logistic Regression** | Baseline interpretable, coeficientes directos |
| **Decision Tree** | Visualizable, fácil de explicar al tribunal |
| **Random Forest** | Mejor performance, feature importance nativa |
| **XGBoost** (opcional) | Estado del arte, muestra dominio del tema |

### Pipeline completo:
```python
from sklearn.pipeline import Pipeline
from sklearn.model_selection import StratifiedKFold, cross_val_score
from sklearn.ensemble import RandomForestClassifier
from sklearn.linear_model import LogisticRegression

# Cross-validation estratificada (importante si hay desbalance de clases)
cv = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)

for model in [LogisticRegression(), RandomForestClassifier(), ...]:
    scores = cross_val_score(model, X, y, cv=cv, scoring='roc_auc')
    print(f"{model.__class__.__name__}: {scores.mean():.3f} ± {scores.std():.3f}")
```

### Métricas a reportar:
- **ROC-AUC** (métrica principal)
- **F1-Score** (si hay desbalance de clases)
- **Matriz de confusión** por modelo
- **Curva ROC** comparativa entre modelos

---

## SECCIÓN 6 — Interpretabilidad
> *Fundamento: Aprendizaje Supervisado + cierre del trabajo*

**Esta sección es la que le da valor real a la tesis.**

Usás **SHAP values** para responder: *¿qué variables son las que más influyen en la predicción?*

```python
import shap

explainer = shap.TreeExplainer(best_model)
shap_values = explainer.shap_values(X_test)

# Summary plot — las features más importantes globalmente
shap.summary_plot(shap_values, X_test)

# Force plot — por qué un dev específico fue clasificado como adoptante
shap.force_plot(explainer.expected_value, shap_values[0], X_test.iloc[0])
```

**Output esperado:** Ranking de las 10 variables más predictivas con interpretación en lenguaje de negocio. Ejemplo: *"Usar VS Code + TypeScript + empresa de +500 empleados es el perfil con mayor probabilidad de adopción sostenida."*

---

## SECCIÓN 7 — NLP (Opcional pero recomendado)
> *Fundamento: Minería de Texto / NLP*

El survey incluye campos de texto libre como respuestas sobre opiniones de IA. Podés:
- Aplicar **análisis de sentimiento** sobre esas respuestas
- Usar **TF-IDF + clustering** para agrupar razones de no adopción
- Comparar el sentimiento textual con la variable target

Esto agrega una dimensión cualitativa al trabajo y justifica la materia de NLP de forma orgánica.

---

## Resumen: Materias → Secciones

| Materia cursada | Sección del trabajo | Técnica concreta |
|---|---|---|
| Análisis Exploratorio | Sección 2 + 3 | EDA, visualizaciones, estadística descriptiva |
| No Supervisado | Sección 4 | K-Means, Silhouette, caracterización de clusters |
| Supervisado | Sección 5 + 6 | Clasificación, CV, ROC-AUC, SHAP values |
| NLP | Sección 7 (opcional) | Sentimiento, TF-IDF sobre respuestas abiertas |
