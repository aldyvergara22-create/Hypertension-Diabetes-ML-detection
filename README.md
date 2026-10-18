# ML Clinical Screening: Predicción de Hipertensión (HTA) y Diabetes Mellitus Tipo 2 (DM2)

Este repositorio contiene la implementación completa del proyecto de Machine Learning orientado al cribado clínico temprano de Hipertensión Arterial (HTA) y Diabetes Mellitus Tipo 2 (DM2) utilizando datos epidemiológicos de salud píblica.

## Objetivo del Proyecto

En el ambito del cribado en salud pública, reducir los falsos negativos es prioritario para evitar diagnósticos tardíos. El objetivo principal es construir modelos predictivos capaces de:

1. Priorizar la capacidad discriminativa global mediante la maximización del AUC-ROC.
2. Garantizar una alta sensibilidad clínica mediante un Recall ≥ 80% en el conjunto de test.
3. Asegurar la capacidad de generalizar del modelo evaluando la estabilidad en la diferencia de Recall (Train-Test <10%).

## Estructura del Repositorio

La arquitectura del proyecto está dividida en fases secuenciales a través de Jupyter Notebooks numerados para asegurar la trazabilidad y la reproducibilidad:

```text
.
├── data/                      # Datasets originales y procesados
├── models/                    # Artefactos y modelos entrenados guardados (.pkl / .joblib)
├── notebooks/                 # Flujo de trabajo interactivo
│   ├── 00_Preparacion...      # Carga, limpieza inicial y estructuración de los datos
│   ├── 01_Exploracion_Dat...  # Análisis Exploratorio de Datos (EDA) y distribución demográfica
│   ├── 02_Preprocesamien...   # Tratamiento de nulos, encoding y estandarización
│   ├── 03_Modelado_Hipe...    # Entrenamiento y selección de modelos para Hipertensión
│   ├── 04_Modelado_Diab...    # Entrenamiento y selección de modelos para Diabetes
│   ├── 05_Evaluacion_Mo...    # Evaluación cruzada, curvas ROC y métricas de HTA
│   ├── 06_Evaluacion_Mo...    # Evaluación cruzada, curvas ROC y métricas de Diabetes
│   ├── 07_SHAP_Hiperten...    # Explicabilidad e interpretabilidad con SHAP para HTA
│   └── 08_SHAP_Diabetes....   # Explicabilidad e interpretabilidad con SHAP para DM2
├── reports/                   # Figuras generadas (Curvas ROC, Boxplots, SHAP plots) y tablas
├── venv/                      # Entorno virtual local (ignorado en Git)
├── .gitignore                 # Archivos excluidos del control de versiones
├── README.md                  # Documentación principal del proyecto
└── requirements.txt           # Dependencias y versiones exactas del entorno
```

Nota sobre los modelos (models/): Debido a los límites de tamaño de archivo de GitHub (>100 MB), los binarios comprimidos de los modelos no están incluidos en el repositorio remoto. Pueden regenerarse fácilmente ejecutando los cuadernos de la carpeta notebooks/ (del 03 al 04).

## Metodología y Principales Hallazgos

Se evaluaron diferentes algoritmos supervisados (Regresión Logística, Random Forest, SVM y XGBoost).

1. Modelos Ganadores Definitivos:

- Hipertensión (HTA): XGBoost Optimizado (Recall = 82,6%, ROC-AUC = 0,8169, Diferencia del Recall = -0,0035).
- Diabetes (DM2): Regresión Logística (class_weight + sample_weight) (Recall = 82,54%, ROC-AUC = 0,8068, Diferencia del Recall = 0,0162).

2. Explicabilidad Médica (SHAP)

- Mediante los notebooks 07_SHAP y 08_SHAP, se analizó la contribución marginal de cada característica biométrica y sociodemográfica, validando la coherencia epidemiológica frente a los sesgos por multicolinealidad.

## Instalación y Reproducción

1. Clonar este repositorio:

git clone https://github.com/aldyvergara22-create/Hypertension-Diabetes-ML-detection.git
cd Hypertension-Diabetes-ML-detection

2. Crear y activar el entorno virtual:

python -m venv venv

### En Windows:

venv\Scripts\activate

### En macOS/Linux:

source venv/bin/activate

3. Instalar las dependencias:

pip install -r requirements.txt

4. Ejecutar los notebooks:

jupyter notebook

Se recomienda ejecutar los cuadernos en el orden numérico indicado (00 a 08). Al ejecutar los notebooks 03 y 04 se volverán a generar los modelos en el directorio models/.

## Autor

Proyecto desarrollado como Trabajo de Fin de Grado enfocado en la aplicación de Machine Learning a la salud pública.
