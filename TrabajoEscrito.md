# **Análisis del Conjunto de Datos Iris**

---

### **Autores**: Jorge Ignacio Gonzalez Valerio |  Victoria Contreras Cambronero

### **Fecha**: Octubre 2024

### **Curso**: Inteligencia Artificial Aplicada

### **Profesor**: ANGELO JESUS ORTIZ VEGA

---

### **Resumen**

Este informe detalla el análisis del conjunto de datos Iris, que incluye un análisis exploratorio de las características, la implementación del modelo K-Nearest Neighbors (KNN) para la clasificación, los resultados obtenidos mediante métricas de evaluación como la precisión y F1-Score, y una discusión sobre los hallazgos y recomendaciones para mejorar el modelo.

## Introducción

El conjunto de datos **Iris** es uno de los más utilizados en el aprendizaje automático para problemas de clasificación. Fue introducido por el estadístico y biólogo Ronald Fisher en 1936 y consiste en 150 muestras de flores de tres especies diferentes: _Iris-setosa_, _Iris-versicolor_ y _Iris-virginica_. Cada muestra incluye cuatro características morfológicas:

- **SepalLengthCm**: Longitud del sépalo en centímetros.
- **SepalWidthCm**: Ancho del sépalo en centímetros.
- **PetalLengthCm**: Longitud del pétalo en centímetros.
- **PetalWidthCm**: Ancho del pétalo en centímetros.

El objetivo de esta tarea es implementar un modelo de clasificación utilizando el algoritmo **K-Nearest Neighbors (KNN)** para predecir la especie de una flor basada en sus características morfológicas. En este informe se detallarán las etapas de análisis exploratorio de los datos, la implementación del modelo, los resultados obtenidos, un análisis de estos resultados y las conclusiones junto con recomendaciones para mejorar el modelo.

## Análisis Exploratorio

Antes de implementar cualquier modelo, es importante explorar el conjunto de datos para entender la distribución de las variables y su relación con la variable objetivo (_Species_). En este caso, se realizaron diversos análisis y visualizaciones para obtener una mejor comprensión.

### 1. Distribución de las Variables

El conjunto de datos Iris contiene cuatro características numéricas. A continuación se presenta un resumen estadístico de las mismas:

![alt text](<res/Pasted image 20241003135505.png>)

Como podemos observar, las características _PetalLengthCm_ y _PetalWidthCm_ tienen una mayor variabilidad en comparación con las demás, lo cual sugiere que pueden ser claves para la clasificación de las especies.

### 2. Visualización de la Distribución de Características

Para visualizar mejor la distribución de las características entre las tres especies de Iris, se crearon gráficos de dispersión y pares (pairplots). Estos gráficos permiten observar cómo se separan las especies en función de las diferentes combinaciones de características. Los resultados mostraron que las especies _Iris-setosa_ están claramente separadas del resto cuando se analizan las variables relacionadas con los pétalos. Sin embargo, las especies _Iris-versicolor_ e _Iris-virginica_ muestran cierta superposición, lo que podría suponer un desafío para el modelo de clasificación.

![alt text](<res/Pasted image 20241003135538.png>)

![alt text](<res/Pasted image 20241003135550.png>)


### 3. Matriz de Correlación

Se calculó la correlación entre las variables y se visualizó mediante un **mapa de calor**. 

![alt text](<res/Pasted image 20241003135700.png>)

La matriz de correlación revela que:

- La longitud del pétalo (_PetalLengthCm_) y el ancho del pétalo (_PetalWidthCm_) están altamente correlacionados con un valor de 0.96.
- Otras características como _SepalLengthCm_ y _SepalWidthCm_ no tienen una correlación tan fuerte entre ellas.

Este análisis sugiere que las características relacionadas con los pétalos son más importantes para la clasificación de las especies.


## Implementación del Modelo

Para este problema de clasificación se utilizó el algoritmo **K-Nearest Neighbors (KNN)**. KNN es un método no paramétrico que utiliza la distancia entre los puntos de datos para hacer predicciones. En este caso, el modelo busca los `k` vecinos más cercanos a un punto de prueba y clasifica el punto en función de la mayoría de las clases presentes entre esos vecinos.

![alt text](<res/Pasted image 20241003140433.png>)

### 1. Preprocesamiento de Datos

- **Normalización**: Dado que las características tienen diferentes escalas, fue necesario normalizar los datos para asegurar que todas las características tuvieran el mismo peso en el cálculo de distancias. Se utilizó la normalización Min-Max para escalar todas las características entre 0 y 1.

### 2. Hiperparámetros del Modelo

Los hiperparámetros son cruciales para el rendimiento del modelo KNN. Los principales hiperparámetros ajustados fueron:

- **Valor de k**: Se realizaron pruebas con varios valores de `k`, y finalmente se eligió **k=3**, ya que proporcionaba un buen equilibrio entre sesgo y varianza. Valores más pequeños de `k` llevaban a un modelo más sensible al ruido, mientras que valores más grandes reducían la capacidad del modelo de captar las diferencias entre las especies.
    
- **Métrica de distancia**: Se utilizó la **distancia Euclidiana** como métrica de distancia, dado que es adecuada para datos normalizados y las características del conjunto Iris.
    

### 3. Validación del Modelo

Se utilizó una **validación cruzada** para evaluar el rendimiento del modelo y asegurar que no estuviera sobreajustado a los datos de entrenamiento. El conjunto de datos fue dividido en **80% para entrenamiento** y **20% para prueba**.

![alt text](<res/Pasted image 20241003135826.png>)

## Resultados

El rendimiento del modelo fue evaluado utilizando varias métricas, que se describen a continuación:

### 1. Precisión del Modelo

El modelo KNN alcanzó una precisión global del **94%**, lo que indica que el 94% de las predicciones fueron correctas.


![alt text](<res/Pasted image 20241003135042.png>)

### 2. F1-Score

El **F1-Score** promedio para las tres clases fue de **0.93**, lo que indica un buen equilibrio entre precisión y recall. Este valor es importante, ya que el modelo no sólo debe ser preciso, sino también consistente en la identificación de las clases.

### 3. Matriz de Confusión

La **matriz de confusión** permite observar los errores cometidos por el modelo. A continuación se presenta la matriz de confusión visualizada como un mapa de calor:

![alt text](<res/Pasted image 20241003134946.png>)

Como se puede observar, el modelo confundió algunas muestras de _Iris-versicolor_ con _Iris-virginica_, lo que sugiere que estas dos especies son más difíciles de separar.
## Análisis de los Resultados Obtenidos

![alt text](<res/Pasted image 20241003140311.png>)


El modelo KNN se desempeñó extremadamente bien con una precisión del 94%, lo que refleja que la mayoría de las muestras fueron clasificadas correctamente. Sin embargo, el pequeño número de errores entre _Iris-versicolor_ e _Iris-virginica_ puede deberse a la similitud entre estas dos especies en cuanto a sus características morfológicas.

- Las características **PetalLengthCm** y **PetalWidthCm** fueron las más útiles para diferenciar las especies, lo que se confirma con los altos valores de correlación observados en la matriz de correlación.
- Se observó una ligera superposición entre las clases de _Iris-versicolor_ e _Iris-virginica_, lo que sugiere que estos datos podrían ser aún más fáciles de clasificar si se utilizan técnicas adicionales como **reducción de dimensionalidad**.

## Conclusiones y Recomendaciones

### Conclusiones

1. El modelo KNN es altamente efectivo para la clasificación del conjunto de datos Iris, logrando una precisión del 94%.
2. Las características relacionadas con los pétalos son las más influyentes para la clasificación, mientras que las características del sépalo aportan menos información discriminatoria.
3. Los errores de clasificación ocurren principalmente entre _Iris-versicolor_ e _Iris-virginica_, debido a su similitud.

### Recomendaciones

1. Se sugiere probar con otros algoritmos de clasificación como **Support Vector Machines (SVM)** o **Random Forest** para comparar resultados y posiblemente mejorar la clasificación.
2. Podría explorarse la reducción de dimensionalidad con técnicas como **PCA** para visualizar mejor la separación entre las especies y reducir el ruido en los datos.
3. Un mayor ajuste de hiperparámetros o incluso el uso de métodos de **búsqueda de hiperparámetros automáticos** como **Grid Search** podría aumentar el rendimiento del modelo.

## Referencias Bibliográficas
- IBM. (2024, octubre 3). What is the k-nearest neighbors (KNN) algorithm? IBM. https://www.ibm.com/mx-es/topics/knn
- Scikit-learn. (2024). Scikit-learn: Machine learning in Python. https://scikit-learn.org/stable/
- Educative. (2024). KNeighborsClassifier in scikit-learn. Educative.io. https://www.educative.io/answers/kneighborsclassifier-in-scikit-learn
- Han, J., Pei, J., & Kamber, M. (2011). Data Mining: Concepts and Techniques (3rd ed.). Morgan Kaufmann.
- Shalev-Shwartz, S., & Ben-David, S. (2014). Understanding Machine Learning: From Theory to Algorithms. Cambridge University Press.

## Rubrica de Evaluacion

| **Criterios**                                              | **Puntuación máxima** | **Puntuación obtenida** |
|------------------------------------------------------------|-----------------------|-------------------------|
| **Descarga y lectura del dataset**                         | 10                    |                         |
| **Análisis de características**                            | 20                    |                         |
| **Implementación de KNN y experimentación de parámetros**  | 30                    |                         |
| **Evaluación del modelo con las métricas recomendadas**    | 15                    |                         |
| **Presentación de los resultados**                         | 15                    |                         |
| **Estructura y claridad del informe**                      | 10                    |                         |
| **Puntos extra (reflexión)**                               | 5                     |                         |

 