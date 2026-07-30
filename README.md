# Predicción de Vulnerabilidad Socioeconómica Global 🌍📊

Este repositorio contiene el código, los datos y la metodología de un proyecto centrado en la creación de un modelo predictivo de vulnerabilidad socioeconómica a nivel global utilizando técnicas de Machine Learning.

## 🎯 Objetivo del Proyecto
Desarrollar un modelo de predicción robusto y riguroso, enfocado en la solidez metodológica, la interpretabilidad de los resultados y una validación técnica exhaustiva para entender los factores determinantes de la vulnerabilidad socioeconómica en diferentes países.

## 📂 Datos y Preprocesamiento
*   **Fuente de Datos:** Banco Mundial (indicadores post-2000).
*   **Estrategia de Limpieza:** Recorte temporal y poda de variables con más de un 80% de valores nulos (Opción 3).
*   **Volumen de Datos Final:** 6,864 registros con una escasez global (*sparsity*) manejada del 25.93%.
*   **Variable Objetivo (Target):** `Target_PCA_100`, un índice sintético de vulnerabilidad generado mediante Análisis de Componentes Principales (PCA).

## 🧠 Modelado y Metodología
El algoritmo principal seleccionado es un **Random Forest Regressor**, elegido por su capacidad para manejar relaciones no lineales y proporcionar una alta interpretabilidad a través de la importancia de variables (*Feature Importance*).

### Optimización de Hiperparámetros
Se ha implementado una búsqueda bayesiana utilizando **Optuna** combinada con Validación Cruzada (5 particiones) para garantizar la máxima capacidad de generalización del modelo, priorizando la robustez frente al sobreajuste.

**Mejores hiperparámetros encontrados:**
| Hiperparámetro | Valor | Descripción |
| :--- | :--- | :--- |
| `n_estimators` | 400 | Número de árboles en el bosque |
| `max_depth` | 38 | Profundidad máxima de cada árbol |
| `min_samples_split` | 3 | Muestras mínimas para dividir un nodo |
| `min_samples_leaf` | 1 | Muestras mínimas en un nodo hoja |
| `max_features` | None | Variables consideradas en cada división |

## 📈 Resultados y Evaluación
El modelo ha sido evaluado sobre un conjunto de prueba (*Test Set*) independiente, demostrando una altísima precisión y control de errores:

*   **R² Score:** 0.9561 (Empate técnico con la media de Validación Cruzada: 0.9576)
*   **RMSE:** 2.8659
*   **MAPE Medio:** 10.48%
*   **Media de Residuos:** -0.04 (Ausencia de sesgo sistemático)

El modelo predice con la misma fiabilidad tanto en países con niveles de vulnerabilidad baja como en aquellos con vulnerabilidad extrema.

## 🔍 Hallazgos Principales (Feature Importance)
El modelo optimizado ha revelado que la vulnerabilidad socioeconómica global se explica predominantemente por factores estructurales de salud pública y calidad institucional, por encima de métricas puramente financieras:

1.  **Mortalidad Infantil (`SH.DYN.MORT`):** Es el indicador dominante (absorbe más del 60% de la capacidad predictiva).
2.  **Mortalidad Materna (`SH.STA.MMRT`).**
3.  **Efectividad Gubernamental (`GOV_WGI_GE_SC`).**
4.  **Estado de Derecho (`GOV_WGI_RL_SC`).**