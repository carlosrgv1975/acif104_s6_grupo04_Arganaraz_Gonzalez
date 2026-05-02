# Prediccion de Accidente Cerebrovascular mediante Machine Learning

**ACIF104 Aprendizaje de Maquinas | Grupo 04 | Universidad Andres Bello**  
Priscila Arganaraz · Carlos Gonzalez · Ingenieria Civil Informatica

---

## DESCRIPCION DEL PROYECTO

Este proyecto tiene como objetivo desarrollar un modelo de Machine Learning capaz de predecir la ocurrencia de accidentes cerebrovasculares (stroke), utilizando variables demograficas y clinicas.

El trabajo fue evaluado en una primera entrega y posteriormente mejorado incorporando nuevas tecnicas, modelos adicionales, explicabilidad con SHAP y una aplicacion web interactiva con Streamlit.

---

## DATASET

Utilizamos el dataset **"Healthcare Stroke Dataset"**, disponible en Kaggle, que contiene informacion de pacientes como:

- Edad, sexo, estado civil
- Nivel de glucosa promedio
- Indice de masa corporal (BMI)
- Tipo de trabajo y tipo de residencia
- Habitos de consumo de tabaco
- Presencia de hipertension y enfermedades cardiacas
- Variable objetivo: `stroke` (1 = tuvo stroke, 0 = no tuvo stroke)

> El dataset presenta un severo desbalance de clases: ~95% clase negativa / ~5% clase positiva.

---

## PROCESAMIENTO DE DATOS

- Identificacion e imputacion de valores nulos en la variable BMI (media de la columna)
- Clasificacion de variables: numericas, categoricas y binarias
- Aplicacion de One-Hot Encoding para variables categoricas
- Calculo de pesos de clase para manejo del desbalance

---

## ANALISIS EXPLORATORIO (EDA)

Incorporado en la version mejorada del notebook:

- Histogramas y boxplots de variables numericas (Edad, Glucosa, BMI)
- Matriz de correlacion entre variables
- Distribucion de edad por clase (Stroke vs No Stroke)
- Graficos de variables categoricas vs clase objetivo (genero, habito de fumar, tipo de trabajo)

---

## MODELAMIENTO

### Version original
Se utilizo **Random Forest** como modelo principal. Se detecto desbalance de clases y se aplico SMOTE como tecnica de correccion.

### Version mejorada (complementaria)
Se amplio el analisis comparando **3 modelos clasicos** con **3 tecnicas de balanceo**:

| Modelo | Recall | F1 | AUC-ROC |
|---|---|---|---|
| Random Forest | 0.00 | 0.000 | 0.785 |
| **Regresion Logistica** | **0.80** | **0.232** | **0.840** |
| XGBoost | 0.12 | 0.129 | 0.764 |
| Red Neuronal (Keras) | 0.80 | 0.223 | 0.821 |

**Modelo seleccionado:** Regresion Logistica con `class_weight='balanced'`  
**Justificacion:** Mayor AUC-ROC (0.840) y mejor recall (0.80) para deteccion de casos de stroke.

### Tecnicas de balanceo comparadas

| Tecnica | Recall | AUC |
|---|---|---|
| class_weight='balanced' | 0.80 | 0.840 |
| SMOTE (sobremuestreo) | 0.80 | 0.841 |
| Undersampling | 0.82 | 0.835 |

---

## RED NEURONAL (KERAS)

Arquitectura implementada: `64 → 32 → 16 → 1`

- Capas Dense con activacion ReLU y Dropout(0.3)
- Salida con activacion Sigmoid (clasificacion binaria)
- Pesos de clase ajustados: `{0: 0.526, 1: 10.268}`
- **AUC-ROC: 0.821**

---

## EXPLICABILIDAD CON SHAP

Se aplico SHAP (SHapley Additive exPlanations) sobre el modelo seleccionado:

- La **edad** es la variable dominante (SHAP ~1.6), con impacto no lineal creciente
- El **nivel de glucosa** es el segundo predictor mas relevante
- La **hipertension** contribuye consistentemente al riesgo predicho
- Resultados consistentes con la evidencia medica existente

---

## APLICACION WEB (STREAMLIT)

Se desarrollo una aplicacion interactiva para prediccion en tiempo real:

- Ingreso de datos del paciente mediante sliders y selectores
- Prediccion de probabilidad de stroke (%)
- Clasificacion de riesgo (Alto / Bajo)
- Visualizacion de variables mas importantes segun SHAP
- Modelo backend: Regresion Logistica con `class_weight='balanced'`

Para ejecutar localmente:
```bash
streamlit run app.py
```

---

## RESULTADOS

### Version original
El modelo Random Forest presento alta precision global, pero bajo desempeno en la deteccion de casos positivos, evidenciando el impacto del desbalance de clases.

### Version mejorada
La Regresion Logistica con `class_weight='balanced'` supero a los demas modelos en las metricas clinicamente relevantes. El analisis SHAP confirmo que la edad es el factor de riesgo dominante para el stroke, en concordancia con la literatura medica.

Ambas versiones demuestran la importancia de abordar el desbalance de clases y de evaluar multiples modelos antes de seleccionar uno para un problema medico.

---

## ARCHIVOS INCLUIDOS

```
├── notebook_v2.ipynb          # Notebook mejorado (58 celdas, ejecutado sin errores)
├── app.py                     # Aplicacion Streamlit
├── dataset/
│   └── healthcare-dataset-stroke-data.csv
├── imagenes/
│   ├── eda_distribuciones.png
│   ├── eda_correlacion.png
│   ├── eda_categoricas.png
│   ├── shap_importancia.png
│   ├── shap_detalle.png
│   └── comparacion_modelos.png
├── informe/
│   └── informe_ACIF104_Grupo04.docx
└── README.md
```

---

## TECNOLOGIAS UTILIZADAS

- Python 3.x
- scikit-learn (Random Forest, Regresion Logistica)
- XGBoost
- TensorFlow / Keras (Red Neuronal)
- imbalanced-learn (SMOTE)
- SHAP
- Streamlit
- pandas, numpy, matplotlib, seaborn

---

## ALUMNOS

| Nombre | Carrera | Universidad |
|---|---|---|
| Priscila Arganaraz | Ingenieria Civil Informatica | UNAB |
| Carlos Gonzalez | Ingenieria Civil Informatica | UNAB |

**Curso:** ACIF104 Aprendizaje de Maquinas  
**Grupo:** 04
