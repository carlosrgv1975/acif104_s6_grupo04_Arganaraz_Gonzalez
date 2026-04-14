# Prediccion de Accidente Cerebrovascular mediante Machine Learning

## DESCRIPCION DEL PROYECTO
Este proyecto tiene como objetivo desarrollar un modelo de Machine Learning capaz de predecir la ocurrencia de accidentes cerebrovasculares (stroke), utilizando variables demograficas y clinicas.

Seguimos la metodologia vista en clases, considerando las etapas de:
- Carga de datos
- Limpieza de datos
- Transformacion
- Modelado
- Evaluacion

---

## DATASET
Utilizamos el dataset "Healthcare Stroke Dataset", que contiene informacion de pacientes como:
- Edad
- Nivel de glucosa
- Indice de masa corporal (BMI)
- Estado civil
- Tipo de trabajo
- Habitos de consumo de tabaco
- Presencia de enfermedades previas

---

## PROCESAMIENTO DE DATOS
- Se identificaron valores nulos en la variable BMI.
- Se imputaron utilizando el promedio de la columna.
- Se clasificaron correctamente las variables (numericas, categoricas y binarias).
- Se aplico One-Hot Encoding para las variables categoricas.

---

## MODELAMIENTO
Utilizamos el algoritmo Random Forest para la construccion del modelo.
Se detecto un problema de desbalance de clases, por lo que decidimos aplicar la tecnica SMOTE para mejorar la deteccion de la clase minoritaria.

---

## RESULTADOS
El modelo inicial presenta alta precision global, pero bajo desempeno en la deteccion de casos positivos.
Luego de aplicar SMOTE, logramos mejorar la capacidad del modelo para identificar casos de stroke.
Esto demuestra la importancia de abordar el desbalance de clases en problemas de clasificacion, especialmente en contextos de salud donde la deteccion de casos positivos es critica.

---

## ARCHIVOS INCLUIDOS
- Notebook del proyecto (.ipynb)
- Dataset utilizado
- PDF del notebook (exportado desde Google Colab)
- Informe final en PDF (de documento Word entregable)
- README del proyecto

---

## ALUMNOS
Priscila Arganaraz
Carlos Gonzalez
Ingenieria Civil Informatica - UNAB