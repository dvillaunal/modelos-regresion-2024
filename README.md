# Modelos de regresión: talleres y proyecto de regresión lineal múltiple (2024-2)

**EN** — Coursework for the *Regression Models* course (Statistics, Universidad Nacional de Colombia, Medellín, semester 2024-2), written as a student in a team of three. It covers multiple linear regression on the Boston Housing data (inference, diagnostics, variable selection, multicollinearity, Ridge, LASSO and PCR), logistic regression on the ISLR `Credit` data, and a car-price modelling project with indicator variables. All reports are Quarto documents rendered to PDF.

**ES** — Trabajos del curso *Modelos de Regresión* (Estadística, Universidad Nacional de Colombia, sede Medellín, semestre 2024-2), elaborados como estudiante en un equipo de tres personas. Incluye regresión lineal múltiple con los datos de vivienda de Boston (inferencia, diagnóstico, selección de variables, multicolinealidad, Ridge, LASSO y PCR), regresión logística con los datos `Credit` de ISLR y un proyecto de modelación del precio de automóviles con variables indicadoras. Todos los informes son documentos Quarto renderizados a PDF.

## Objetivo

Aplicar el ciclo completo de un modelo de regresión: plantear y ajustar el modelo, probar hipótesis sobre sus parámetros, validar supuestos, diagnosticar observaciones atípicas, de balanceo e influenciales, tratar la multicolinealidad, seleccionar variables y construir intervalos de confianza y de predicción.

## Datos

Todos los datos usados están incluidos en el repositorio o se cargan desde paquetes de R.

| Trabajo | Datos | Tamaño usado | Respuesta y predictoras |
|---|---|---|---|
| Talleres 1 y 2 | Boston Housing (`boston.csv`) | Filas 401 a 500 (100 viviendas) de 506 | `MEDV` frente a `CRIM`, `NOX`, `RM`, `AGE`, `PTRATIO`, `LSTAT` |
| Taller 4 | `Credit` del paquete `ISLR` | Filas 30 a 95 (66 personas) | `Married` (sí/no) frente a `Rating` |
| Proyecto | [Car Price Prediction (Kaggle)](https://www.kaggle.com/datasets/hellbuoy/car-price-prediction/data), `CarPrice_Assignment.csv` | 205 autos, 26 variables, sin faltantes | `price` frente a variables técnicas (ancho, tamaño del motor, potencia, tracción, etc.) |

## Métodos

- **Taller 1 (RLM, parte 1):** ajuste por mínimos cuadrados, tabla ANOVA, pruebas t individuales, prueba de sumas de cuadrados extra, sumas de cuadrados tipo I y II, residuales estudentizados, gráfico Q-Q, leverage y distancia de Cook, reajuste sin observaciones problemáticas.
- **Taller 2 (RLM, parte 2):** diagnóstico de multicolinealidad (matriz de correlación, VIF, índice de condición, proporciones de varianza); selección por $R^2_{adj}$, $C_p$, stepwise, forward y backward; Ridge y LASSO con validación cruzada (`glmnet`); regresión por componentes principales (`pls`).
- **Taller 3 (en `Proyecto2.qmd`):** modelo con variable indicadora e interacción (`price ~ carwidth * drivewheel`), pruebas de igualdad de interceptos, de pendientes y de coincidencia de rectas (test lineal general), Shapiro-Wilk y Breusch-Pagan.
- **Taller 4:** regresión logística (`glm`, familia binomial), razón de odds, prueba frente al modelo nulo, intervalos para la probabilidad y tasa de clasificación correcta.
- **Proyecto (tres entregas):** análisis descriptivo y limpieza (nombre de la marca a partir de `CarName`), RLM con covariables continuas, coeficientes estandarizados, diagnóstico de residuales y de observaciones influyentes, multicolinealidad, selección de variables e intervalos de confianza y predicción al 90 %.

## Resultados principales

- **Taller 1:** el modelo con seis predictoras explica el 60,35 % de la variabilidad de `MEDV`; `CRIM`, `NOX` y `LSTAT` son significativas, y la prueba de sumas de cuadrados extra no rechaza que `RM`, `AGE` y `PTRATIO` sean no significativas en conjunto (p = 0,837). Retirar las observaciones problemáticas no cambia de forma sustancial las conclusiones.
- **Taller 2:** no hay evidencia de multicolinealidad severa. Todos los métodos de selección eligen `CRIM`, `NOX` y `LSTAT` ($R^2_{adj}$ = 0,587). MSE: LASSO 11,31; Ridge 11,40; PCR con 3 componentes 12,03.
- **Taller 3:** por separado, no hay evidencia de interceptos distintos (p = 0,1227) ni de pendientes distintas entre los niveles de `drivewheel`; la prueba conjunta de coincidencia de rectas sí se rechaza (p = 2,2e-10). Los residuales no cumplen normalidad (Shapiro-Wilk) ni homocedasticidad (Breusch-Pagan).
- **Taller 4:** `Rating` es significativa (p = 0,026); el odds ratio por unidad de rating es 1,0053 y el modelo clasifica correctamente el 59 % de las observaciones.
- **Proyecto:** el modelo con covariables continuas explica el 62,48 % de la variabilidad del precio. Con todas las covariables numéricas aparece multicolinealidad severa en algunas; los mejores modelos alcanzan $R^2_{adj}$ = 0,841. Se propone el modelo backward (`carwidth`, `enginesize`, `stroke`, `compressionratio`, `horsepower`, `peakrpm`) por parsimonia, con la advertencia de que ninguno de los modelos candidatos cumple todos los supuestos. Para un auto promedio, el precio estimado es 13.354 (IC 90 % de la media: 12.975,58 a 13.732,42; intervalo de predicción 90 %: 7.975,62 a 18.732,37).

## Estructura del repositorio

```
Taller_1/
  Taller_4.qmd / .pdf          Taller 1 (RLM parte 1); el archivo conserva un nombre heredado
  Bases_de_datos/boston.csv    Datos de vivienda de Boston
  Script1DatosSeleccionPersonal.R  Script de ejemplo de clase
Taller_2/
  Taller_2.qmd / .pdf          Taller 2 (multicolinealidad, selección, Ridge, LASSO, PCR)
  boston.csv                   Copia de los datos de Boston
Taller_4/
  Taller_4.qmd / .pdf          Taller 4 (regresión logística, datos Credit)
Proyecto_RLM/
  Proyecto.qmd / .pdf          Proyecto de RLM, entregas 1 a 3 (precio de automóviles)
  Proyecto2.qmd / .pdf         Taller 3: variables indicadoras e interacción
  CarPrice_Assignment.csv      Datos del proyecto
  ScriptREjemploMRLMIndicadoras.R  Script de ejemplo de clase (variables indicadoras)
  portada.tex                  Portada LaTeX compartida
```

Las carpetas `*_cache/` y `*_files/` son salidas intermedias de Quarto.

## Cómo reproducir

- **Software:** R y Quarto con una distribución de LaTeX (salida PDF). La versión de R no está registrada en el repositorio.
- **Paquetes:** `tidyverse`, `magrittr`, `car`, `olsrr`, `leaps`, `glmnet`, `pls`, `rsm`, `GGally`, `corrplot`, `psych`, `lmtest`, `ISLR`, `janitor`, `skimr`, `DataExplorer`, `gridExtra`, `kableExtra`, `knitr`, `xtable`, `pander`, `glue`, `scales`, `hrbrthemes`, `rgl`, `scatterplot3d`, `reticulate`, `forcats`, `stringr`.
- **Funciones auxiliares:** el proyecto carga `FuncionesdeUsuarioRLM.R` desde el repositorio público [NelfiGonzalez/Regresion-DOE](https://github.com/NelfiGonzalez/Regresion-DOE), por lo que requiere conexión a internet.
- **Ejecución:** abrir el `.Rproj` de cada carpeta y renderizar el documento, por ejemplo `quarto render Proyecto_RLM/Proyecto.qmd`.

## Contexto y autoría

Trabajos presentados como estudiantes del curso *Modelos de Regresión*, Departamento de Estadística, Facultad de Ciencias, Universidad Nacional de Colombia, sede Medellín, semestre 2024-2 (entregas entre diciembre de 2024 y febrero de 2025).

Autores: Daniel Felipe Villa Rengifo, Luis David Hernández Pérez y Juan Gabriel Carvajal Negrete.

Licencia: GPL-3.0 (ver `LICENSE`).
