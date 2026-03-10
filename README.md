# Challenge Telecom X 2 - Predicción de Cancelación de Clientes

Este proyecto corresponde a la segunda parte del desafío **Telecom X**, enfocado en la construcción de modelos de **Machine Learning** para predecir la cancelación de clientes (**churn**).

A partir del dataset previamente tratado en la primera parte del challenge, se desarrolló un flujo de trabajo que incluyó preprocesamiento, análisis exploratorio orientado al modelado, entrenamiento de modelos de clasificación, evaluación de métricas e interpretación de variables relevantes para generar hallazgos accionables de negocio.

---

## Objetivo

Desarrollar modelos predictivos capaces de identificar clientes con mayor probabilidad de cancelar sus servicios, con el fin de ayudar a Telecom X a anticiparse al churn y diseñar estrategias de retención más efectivas.

---

## Contenido del proyecto

En este notebook se trabajó con las siguientes etapas:

- Carga del dataset tratado de la Parte 1
- Eliminación de columnas irrelevantes
- Transformación de variables categóricas mediante **one-hot encoding**
- Verificación de proporción de cancelación y análisis de desbalance de clases
- Justificación del uso o no de técnicas de balanceo
- Análisis de correlación entre variables
- Análisis dirigido de variables clave:
  - Tiempo de permanencia × Cancelación
  - Gasto total × Cancelación
- División del dataset en entrenamiento y prueba
- Entrenamiento de modelos de clasificación
- Evaluación con métricas de desempeño
- Análisis de importancia de variables
- Conclusiones y propuestas estratégicas de retención

---

## Dataset

El análisis se realizó sobre un dataset limpio y tratado previamente, con aproximadamente **7032 registros** y variables relacionadas con:

- perfil del cliente
- servicios contratados
- tipo de contrato
- método de pago
- cargos mensuales y totales
- cancelación del servicio (`Churn`)

La variable objetivo del proyecto es:

- `Churn`
  - `0`: cliente permanece activo
  - `1`: cliente canceló el servicio

---

## Preprocesamiento realizado

Durante la preparación de datos se aplicaron los siguientes pasos:

### 1. Eliminación de variables irrelevantes
Se eliminó la columna `customerID`, ya que corresponde a un identificador único y no aporta valor predictivo al modelo.

### 2. Codificación de variables categóricas
Se aplicó **one-hot encoding** a las columnas categóricas que aún se encontraban en formato texto, utilizando `pd.get_dummies()`.

### 3. Revisión del desbalance de clases
Se verificó la distribución de la variable `Churn`, encontrando un **desbalance moderado**:

- Clientes activos: **73.42%**
- Clientes que cancelaron: **26.58%**

No se aplicó balanceo en esta etapa, pero se dejó justificada su posible utilización en futuras iteraciones.

### 4. Normalización / estandarización
Se justificó la necesidad de aplicar estandarización únicamente en modelos sensibles a la escala de las variables, como **Regresión Logística**.  
Los modelos basados en árboles fueron entrenados sin normalización.

---

## Modelos utilizados

Se entrenaron dos modelos de clasificación:

### 1. Regresión Logística
Modelo lineal e interpretable, sensible a la escala de las variables, por lo que se trabajó con estandarización en las variables numéricas continuas.

### 2. Random Forest
Modelo basado en árboles, no sensible a la escala de los datos y capaz de capturar relaciones no lineales.

---

## Evaluación de modelos

Los modelos fueron evaluados con las siguientes métricas:

- Accuracy
- Precision
- Recall
- F1-score
- Matriz de confusión

### Resultados principales

#### Regresión Logística
- **Accuracy:** 0.8033
- **Precision:** 0.6594
- **Recall:** 0.5383
- **F1-score:** 0.5927

#### Random Forest
- **Accuracy:** 0.7825
- **Precision:** 0.6186
- **Recall:** 0.4742
- **F1-score:** 0.5368

### Conclusión del desempeño
La **Regresión Logística** obtuvo mejor desempeño general en el conjunto de prueba, superando a Random Forest en todas las métricas principales.

Además, Random Forest presentó señales claras de **overfitting**, al obtener una exactitud muy alta en entrenamiento pero una caída importante en prueba.

---

## Hallazgos principales

A partir del análisis de correlación, los coeficientes de la Regresión Logística y la importancia de variables de Random Forest, se identificaron factores relevantes asociados a la cancelación.

### Factores asociados a mayor churn
- menor antigüedad del cliente (`customer.tenure`)
- contratos mes a mes
- servicio de internet por **fibra óptica**
- método de pago **Electronic check**
- facturación electrónica (`PaperlessBilling`)
- mayores cargos mensuales

### Factores asociados a menor churn
- mayor tiempo de permanencia
- contratos de **uno o dos años**
- servicios de valor agregado como:
  - `OnlineSecurity`
  - `TechSupport`
- algunos perfiles con partner o dependientes

### Observaciones adicionales
También se observó que los clientes que cancelan tienden a presentar:

- menor antigüedad
- menor gasto total acumulado

Esto sugiere que una parte importante del churn ocurre en etapas relativamente tempranas de la relación con la empresa.

---

## Estrategias de retención propuestas

Con base en los resultados del análisis, se proponen las siguientes acciones para Telecom X:

1. **Fortalecer la retención temprana**  
   Diseñar estrategias para clientes nuevos durante los primeros meses de permanencia.

2. **Incentivar contratos de mayor duración**  
   Promover migraciones de contratos mensuales a planes de uno o dos años.

3. **Monitorear perfiles con mayor riesgo**  
   En especial clientes con:
   - fibra óptica
   - pago mediante Electronic check
   - cargos mensuales más altos

4. **Promover servicios complementarios**  
   Fomentar la adopción de servicios como soporte técnico y seguridad online, asociados a menor churn.

5. **Usar modelos predictivos para campañas preventivas**  
   Priorizar acciones comerciales o de fidelización sobre clientes con alta probabilidad de cancelación.

---

## Estructura sugerida del repositorio

📁 telecomx-churn-ml
│
├── Challenge_TelecomX_2.ipynb
├── datos_telecomx_limpios.csv
└── README.md

---

## Tecnologías y librerías utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn

---

## Cómo ejecutar el proyecto

1. Clona este repositorio:
```
git clone <URL_DEL_REPOSITORIO>
```

2. Entra al directorio del proyecto:

```
cd telecomx-churn-ml
```
3. Instala las dependencias necesarias:

```
pip install pandas numpy matplotlib seaborn scikit-learn
```
3. Abre el notebook:
```
jupyter notebook
```
4. Ejecuta el archivo:
```
Challenge_TelecomX_2.ipynb
```

## Próximos pasos

Como mejora futura, este proyecto podría ampliarse con:

- Ajuste de hiperparámetros
- Validación cruzada
- Balanceo de clases con SMOTE
- Optimización de umbrales de clasificación
- Prueba de modelos adicionales como XGBoost, SVM o KNN

## Autor

**José Felipe Guillén**

Proyecto desarrollado como parte del programa de formación de Oracle / Alura, en el desafío Telecom X orientado a análisis predictivo de churn.