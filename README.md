# Telecom X - Parte 2: Prediccion de Cancelacion (Churn)

## Proposito del analisis

Este proyecto desarrolla modelos predictivos para estimar la probabilidad de cancelacion (churn) de clientes en Telecom X.

Objetivo principal:

- Anticipar clientes con mayor riesgo de churn.
- Identificar variables mas influyentes.
- Proponer estrategias de retencion basadas en evidencia.

## Estructura del proyecto

- `TelecomX_Parte2_Modelos_Churn.ipynb`: notebook principal de modelado, evaluacion e interpretacion.
- `datos_tratados.csv`: dataset tratado de la Parte 1 (si no existe, el notebook lo genera de forma consistente desde `TelecomX_Data.json`).

## Preparacion de datos para modelado

1. Carga del archivo tratado:

- Se prioriza el CSV tratado de Parte 1 para mantener continuidad analitica.
- Si no existe, se reconstruye con el mismo criterio de ETL de Parte 1 y se exporta como `datos_tratados.csv`.

2. Eliminacion de columnas irrelevantes:

- Se elimina `customerID` por ser identificador unico sin valor predictivo.

3. Variable objetivo:

- Se estandariza `Churn` en `Yes/No` y se crea `churn_bin` (1=Yes, 0=No).

4. Clasificacion de variables:

- Numericas: `tenure`, `Charges.Monthly`, `Charges.Total`, `Cuentas_Diarias`, `NumServicios`, etc.
- Categoricas: `Contract`, `PaymentMethod`, `InternetService`, `OnlineSecurity`, etc.

5. Encoding:

- Se aplica `OneHotEncoder` para transformar categoricas a numericas en los pipelines.

6. Escalado:

- Regresion Logistica: incluye `StandardScaler` (modelo sensible a escala).
- Random Forest: sin escalado (modelo basado en arboles, no sensible a magnitud).

7. Separacion train/test:

- Se utiliza split 80/20 con estratificacion para conservar proporcion de churn en ambos conjuntos.

## Modelos implementados

Se entrenan al menos dos modelos:

- `LogisticRegression` (con escalado, `class_weight='balanced'`).
- `RandomForestClassifier` (sin escalado, `class_weight='balanced_subsample'`).

## Evaluacion de modelos

Metricas reportadas para cada modelo:

- Exactitud (accuracy)
- Precision
- Recall
- F1-score
- Matriz de confusion

Analisis adicional:

- Comparacion `train_score` vs `test_score` para detectar overfitting o underfitting.

## Analisis de correlacion y analisis dirigido

- Matriz de correlacion para variables numericas y correlacion con `churn_bin`.
- Analisis dirigido de:
  - `tenure x Churn`
  - `Charges.Total x Churn`
- Visualizaciones: boxplots y scatter plot (muestra) para identificar patrones de riesgo.

## Importancia de variables

- Regresion Logistica: interpretacion de coeficientes (magnitud y signo).
- Random Forest: `feature_importances_` para ranking de variables.

## Insights y conclusion estrategica

El notebook finaliza con un resumen ejecutivo automatico que:

- Recomienda el mejor modelo por F1-score.
- Resume riesgos de ajuste (overfitting/underfitting).
- Destaca factores de mayor impacto en churn.
- Propone estrategias de retencion accionables.

## Como ejecutar

1. Abre `TelecomX_Parte2_Modelos_Churn.ipynb`.
2. Ejecuta celdas en orden desde la primera hasta la ultima.
3. Revisa tablas de metricas, matrices de confusion e importancia de variables.
4. Usa la conclusion final para justificar decisiones de negocio.

## Dependencias

Instala librerias necesarias:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn jupyter
```

## Git y GitHub (entrega)

Comandos recomendados para versionar el progreso:

```bash
git pull
git add .
git commit -m "Parte 2: modelos predictivos de churn"
git push
```
