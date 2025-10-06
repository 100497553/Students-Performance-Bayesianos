# Students-Performance-Bayesianos

# Naive Bayes
El clasificador Naive Bayes es un modelo de aprendizaje automático basado en el teorema de Bayes, utilizado principalmente para problemas de clasificación. Este método es especialmente efectivo en aplicaciones con datos categóricos y mixtos porque trabaja bajo el principio "naïve" al suponer que todas las características de entrada son independientes entre sí, aunque en la práctica puedan no serlo.

El teorema de Bayes proporciona una forma de calcular la probabilidad de que ocurra un evento dado otro evento ya observado. En el contexto de Naive Bayes, se calcula la probabilidad de que una clase (en este caso, "aprobado" o "no aprobado") sea la correcta para una observación considerando la probabilidad de las características que contiene.

# Librería e1071
La librería e1071 en R es conocida por su implementación de varios algoritmos de aprendizaje automático, incluyendo el modelo Naive Bayes, que es particularmente útil para problemas de clasificación con variables mixtas (categóricas y numéricas).
Resultados obtenidos en R:
Matriz de Confusión - e1071:
        Real
Predicho  No  Sí
      No  70  10
      Sí   1 168

Precisión: 0.9558
Sensibilidad (Recall - Sí): 0.9438
Especificidad (Recall - No): 0.9859
El modelo muestra un excelente rendimiento con una precisión del 95.58%, identificando correctamente 238 de las 249 observaciones de prueba. La especificidad del 98.59% indica una capacidad casi perfecta para detectar estudiantes que no aprueban, mientras que la sensibilidad del 94.38% demuestra una alta efectividad en identificar a los que sí aprueban.

# Librería klaR
La librería klaR en R está diseñada para facilitar la clasificación y análisis estadístico, con un enfoque particular en la clasificación Naive Bayes. Sin embargo, esta implementación requiere que todas las variables sean factores, lo que nos obligó a discretizar las variables numéricas.
Proceso de discretización:
Convertimos las puntuaciones continuas en 5 categorías:
Muy_Bajo, Bajo, Medio, Alto, Muy_Alto
Resultados obtenidos en R:
Matriz de Confusión - klaR:
        Real
Predicho  No  Sí
      No  71  42
      Sí   0 136

Precisión: 0.8313
Sensibilidad (Recall - Sí): 0.7640
Especificidad (Recall - No): 1.0000
El modelo con klaR muestra un rendimiento inferior (83.13% de precisión) debido principalmente a la pérdida de información durante la discretización. Aunque logra una especificidad perfecta (100%), su sensibilidad es significativamente más baja (76.40%), indicando dificultades para identificar correctamente a los estudiantes que aprueban.

# Suavización de Laplace
La suavización de Laplace es una técnica utilizada para evitar que las probabilidades de ocurrencia de ciertas características dentro de una clase se vuelvan cero, lo que podría invalidar las predicciones. Consiste en agregar una constante positiva (en este caso 1) al número de ocurrencias de cada característica antes de calcular las probabilidades.
Resultados con Laplace en R
Precisión con Laplace: 0.9558
En este caso, la suavización de Laplace no mejora la precisión del modelo, lo que sugiere que el conjunto de datos es suficientemente grande y no presenta problemas de probabilidades cero.

# Comparativa de resultados
Modelo	           Precisión	Sensibilidad	Especificidad	Tiempo (segundos)
e1071	               0.9558	     0.9438	        0.9859	       0.03
klaR	               0.8313	     0.7640	        1.0000	       0.00
e1071 + Laplace	     0.9558	        -	             -	           -
# Análisis detallado del mejor modelo (e1071)
Métricas por clase:
Precisión para "Sí": 99.41%
Precisión para "No": 87.50%
Desglose de clasificaciones:
Verdaderos Positivos: 168
Falsos Positivos: 1
Falsos Negativos: 10
Verdaderos Negativos: 70

# Conclusiones
Una vez aplicadas las diferentes implementaciones de Naive Bayes, obtenemos resultados significativamente distintos. En primer lugar, hemos medido los tiempos de ejecución de los modelos, obteniendo que klaR es ligeramente más rápido, pero esta ventaja es irrelevante dado su menor precisión.
El modelo implementado con e1071 demuestra un rendimiento excepcional, clasificando correctamente el 95.58% de las observaciones. Específicamente:
Clasifica correctamente 168/178 = 94.38% de los estudiantes aprobados
Clasifica correctamente 70/71 = 98.59% de los estudiantes no aprobados
El modelo con klaR, aunque más rápido, presenta una precisión significativamente menor (83.13%), principalmente debido a la necesidad de discretizar las variables numéricas, lo que causa pérdida de información y genera el warning "Numerical 0 probability for all classes" observado durante las predicciones.
La suavización de Laplace no produce mejoras en este caso, lo que indica que el tamaño del conjunto de datos es suficiente para estimar probabilidades confiables sin necesidad de ajustes adicionales.

# Factores que contribuyen al éxito del modelo:
Las variables numéricas (scores) tienen alta capacidad predictiva
Las variables categóricas aportan información complementaria valiosa
El tamaño del conjunto de datos permite estimaciones robustas
A pesar del supuesto de independencia, las variables individualmente son suficientemente informativas

# Recomendaciones para uso futuro:
Preferir la implementación e1071 por su manejo nativo de variables mixtas
Evitar la discretización de variables numéricas cuando sea posible
Validar la necesidad de suavización según las características del dataset
Considerar técnicas para manejar el desbalance de clases en futuras iteraciones

En conclusión, el clasificador Naive Bayes implementado con e1071 demuestra ser una herramienta efectiva y eficiente para predecir el rendimiento académico, logrando una alta precisión a pesar del supuesto de independencia entre variables. Su implementación simple y rápida ejecución lo convierten en una opción recomendable para problemas de clasificación similares en el ámbito educativo.
