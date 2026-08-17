<a id="english-version"></a>

# 🎬 IMDb Review Sentiment Classification

[View Spanish version](#spanish-version)

## Overview

This analysis develops a natural language processing solution to automatically classify IMDb movie reviews as positive or negative.

The work compares multiple machine learning approaches to determine which alternative provides the strongest balance between predictive performance, interpretability, and computational efficiency.

## Business Context

Film Junky Union requires an efficient way to organize large volumes of user-generated reviews and identify negative feedback automatically.

A reliable sentiment classification system can support:

* Early identification of negative audience reactions.
* Prioritization of reviews requiring further analysis.
* Monitoring of customer perception at scale.
* More efficient analysis of qualitative feedback.

## Analytical Objective

Build and evaluate sentiment classification models capable of identifying positive and negative movie reviews from unstructured text.

The required performance threshold was an F1 score of at least **0.85** on the test dataset.

## Dataset

The analysis uses **47,331 IMDb movie reviews** with labeled sentiment information.

Key characteristics:

* 23,796 training records.
* 23,535 test records.
* Nearly balanced distribution between positive and negative reviews.
* No missing values in the review text.
* No duplicated records.
* Predefined training and test partitions.

The dataset is not included in this repository.

## Methodology

The analytical workflow included:

1. Data quality assessment and structural validation.
2. Exploratory analysis of reviews, ratings, sentiment, and temporal distribution.
3. Text normalization and removal of non-alphabetic characters.
4. TF-IDF vectorization with a maximum vocabulary of 50,000 features.
5. Lemmatization with spaCy for selected models.
6. Training and comparison of baseline, linear, and boosting classifiers.
7. Evaluation using Accuracy, F1, Average Precision, and ROC AUC.
8. Qualitative assessment with additional positive, negative, and mixed reviews.

## Models Evaluated

| Model    | Text Processing                | Algorithm           |
| -------- | ------------------------------ | ------------------- |
| Baseline | Constant input                 | Dummy Classifier    |
| Model 1  | Normalization and TF-IDF       | Logistic Regression |
| Model 3  | spaCy lemmatization and TF-IDF | Logistic Regression |
| Model 4  | spaCy lemmatization and TF-IDF | LightGBM            |

BERT was considered but not implemented because the traditional models already exceeded the required performance threshold with substantially lower computational requirements.

## Results

| Model                                | Train F1 | Test F1 | Test ROC AUC |
| ------------------------------------ | -------: | ------: | -----------: |
| Dummy Classifier                     |     0.00 |    0.00 |         0.50 |
| TF-IDF + Logistic Regression         |     0.94 |    0.88 |         0.95 |
| spaCy + TF-IDF + Logistic Regression |     0.93 |    0.88 |         0.95 |
| spaCy + TF-IDF + LightGBM            |     0.99 |    0.88 |         0.95 |

All trained models exceeded the required test F1 threshold of **0.85**.

## Recommended Model

The recommended solution is **TF-IDF with Logistic Regression**.

It provides the most favorable balance between:

* Predictive performance.
* Generalization to unseen reviews.
* Computational efficiency.
* Interpretability.
* Maintenance simplicity.

Lemmatization did not produce a measurable improvement in test performance. LightGBM achieved a higher training score but did not outperform Logistic Regression on the test dataset, indicating greater overfitting without additional business value.

## Business Implications

The selected model can support the automated organization and prioritization of customer feedback. Its efficient architecture makes it suitable as a baseline for sentiment monitoring without requiring the infrastructure associated with deep learning models.

Before operational use, the classification threshold should be aligned with the cost of false positives and false negatives. Performance should also be monitored as audience vocabulary and review patterns evolve.

## Technologies

* Python
* pandas
* NumPy
* scikit-learn
* NLTK
* spaCy
* LightGBM
* Matplotlib
* Seaborn
* Jupyter Notebook

## Repository Structure

```text
imdb_review_sentiment_classification/
│
├── imdb_sentiment_classification_model.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## Author

**Carolina Caycho**

[GitHub Profile](https://github.com/Carolg3456)

---

<a id="spanish-version"></a>

# 🎬 Clasificación de Sentimiento en Reseñas de IMDb

[Ver versión en inglés](#english-version)

## Descripción general

Este análisis desarrolla una solución de procesamiento de lenguaje natural para clasificar automáticamente las reseñas de películas de IMDb como positivas o negativas.

Se comparan distintos enfoques de machine learning para determinar qué alternativa ofrece el mejor equilibrio entre rendimiento predictivo, interpretabilidad y eficiencia computacional.

## Contexto de negocio

Film Junky Union necesita organizar grandes volúmenes de opiniones generadas por sus usuarios e identificar automáticamente los comentarios negativos.

Un sistema confiable de clasificación de sentimiento puede contribuir a:

* Detectar oportunamente reacciones negativas de la audiencia.
* Priorizar reseñas que requieran un análisis más detallado.
* Monitorear la percepción de los usuarios a escala.
* Analizar comentarios cualitativos con mayor eficiencia.

## Objetivo analítico

Construir y evaluar modelos de clasificación de sentimiento capaces de identificar reseñas positivas y negativas a partir de texto no estructurado.

El criterio mínimo establecido fue alcanzar un valor F1 de **0.85** en el conjunto de prueba.

## Datos

El análisis utiliza **47,331 reseñas de películas de IMDb** etiquetadas según su sentimiento.

Características principales:

* 23,796 registros de entrenamiento.
* 23,535 registros de prueba.
* Distribución prácticamente equilibrada entre reseñas positivas y negativas.
* Ausencia de valores faltantes en el texto de las reseñas.
* Ausencia de registros duplicados.
* Particiones predefinidas de entrenamiento y prueba.

El dataset no está incluido en este repositorio.

## Metodología

El flujo analítico comprendió:

1. Evaluación de calidad y validación estructural de los datos.
2. Análisis exploratorio de reseñas, puntuaciones, sentimiento y distribución temporal.
3. Normalización del texto y eliminación de caracteres no alfabéticos.
4. Vectorización TF-IDF con un vocabulario máximo de 50,000 características.
5. Lematización mediante spaCy para modelos seleccionados.
6. Entrenamiento y comparación de clasificadores base, lineales y boosting.
7. Evaluación mediante Accuracy, F1, Average Precision y ROC AUC.
8. Evaluación cualitativa con reseñas adicionales positivas, negativas y mixtas.

## Modelos evaluados

| Modelo     | Procesamiento del texto         | Algoritmo           |
| ---------- | ------------------------------- | ------------------- |
| Línea base | Entrada constante               | Dummy Classifier    |
| Modelo 1   | Normalización y TF-IDF          | Regresión logística |
| Modelo 3   | Lematización con spaCy y TF-IDF | Regresión logística |
| Modelo 4   | Lematización con spaCy y TF-IDF | LightGBM            |

BERT fue considerado, pero no implementado porque los modelos tradicionales superaron el rendimiento mínimo requerido con necesidades computacionales considerablemente menores.

## Resultados

| Modelo                               | F1 entrenamiento | F1 prueba | ROC AUC prueba |
| ------------------------------------ | ---------------: | --------: | -------------: |
| Dummy Classifier                     |             0.00 |      0.00 |           0.50 |
| TF-IDF + regresión logística         |             0.94 |      0.88 |           0.95 |
| spaCy + TF-IDF + regresión logística |             0.93 |      0.88 |           0.95 |
| spaCy + TF-IDF + LightGBM            |             0.99 |      0.88 |           0.95 |

Todos los modelos entrenados superaron el umbral mínimo de **0.85** para el valor F1 en prueba.

## Modelo recomendado

La solución recomendada es **TF-IDF con regresión logística**.

Ofrece el balance más favorable entre:

* Rendimiento predictivo.
* Generalización ante nuevas reseñas.
* Eficiencia computacional.
* Interpretabilidad.
* Facilidad de mantenimiento.

La lematización no produjo una mejora medible en el rendimiento de prueba. LightGBM alcanzó un resultado superior en entrenamiento, pero no superó a la regresión logística en prueba, lo que evidencia mayor sobreajuste sin aportar valor adicional.

## Implicaciones para el negocio

El modelo seleccionado puede apoyar la organización y priorización automática de comentarios de clientes. Su arquitectura eficiente permite utilizarlo como base para monitorear el sentimiento sin requerir la infraestructura asociada con modelos de aprendizaje profundo.

Antes de utilizarlo operativamente, el umbral de clasificación debe alinearse con el costo de los falsos positivos y falsos negativos. También será necesario monitorear el rendimiento conforme evolucionen el vocabulario de los usuarios y los patrones de las reseñas.

## Tecnologías

* Python
* pandas
* NumPy
* scikit-learn
* NLTK
* spaCy
* LightGBM
* Matplotlib
* Seaborn
* Jupyter Notebook

## Estructura del repositorio

```text
imdb_review_sentiment_classification/
│
├── imdb_sentiment_classification_model.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## Autora

**Carolina Caycho**

[Perfil de GitHub](https://github.com/Carolg3456)
