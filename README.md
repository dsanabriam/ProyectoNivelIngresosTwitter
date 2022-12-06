# Modelo de Predicción del Nivel de Ingresos basado en modelos de procesamiento de lenguaje natural en redes sociales digitales “Twitter”

## Por 
## Diana Sanabria 
## Laura Nuñez
## Camilo Peñaranda 

# Tabla de contenido

1. [Definición del proyecto](#definition)
2. [Analisis](#analysis)
3. [Conclusiones](#conclusion)


# Definición del proyecto <a name="definition"></a>

## Descripción del proyecto

Desarrollar un modelo de clasificación que permita la identificación de perfiles por niveles de ingreso (alto, medio, bajo) a partir de la información registrada en Twitter de una persona para el otorgamiento de créditos. 

## Desarrollo del proyecto 
Se obtuvieron 2.7 millones de textos extraidos de Twitter mediante el uso de API´s los cuales que se almacenaron en Mongo DB para posteriormente hacer un preprocesamiento de estos datos no estructurados. Para lo antetrior, se usaron técnicas de NLP.  
Posteriormente, se probaron varios algoritmos para predecir no solo el nivel de ingreso, sino también las variables demográficas de interés que harán parte del dataset de entrada, adicionando el texto tratado mediante NLP descrito anteriormente.

### Métricas 

Para este proyecto se usara el accuracy del base de pruebas como medida de desempeño para escoger el mejor modelo. 

# Analisis <a name="analysis"></a>

#### Descriptivas 
Hay un total de 1031 usuarios únicos de Twitter.  
Hay un total de 2.7 millones de textos. 

Género: Esta variable se completó de manera heurística considerando la información que estaba publicada, clasificándola en hombre o mujer. Siendo así, 652 usuarios son hombres y 379 mujeres. 

Nivel de Ingresos: Para determinar el nivel de ingresos se tomó como referencia la profesión, la edad y el género. De la siguiente forma: 

Se realizó la extracción de información de los salarios según las profesiones de Talent.com6 correspondiente a una página de reclutamiento laboral en Colombia.   

Se consultó en el Departamento Administrativo Nacional de Estadística (DANE) 7 la brecha salarial según género, en donde para las mujeres se encuentra una brecha salarial de 23.9% por debajo con respecto al salario que devengan los hombres.    

Se consultó en el DANE la brecha salarial según género y edad, agrupado por rangos de edad. 

Se graficó y analizó la distribución estadística de los niveles de ingresos de las 1.301 cuentas de usuarios del estudio, ubicándolos en percentiles. 

Segmentación de la variable Nivel de Ingresos: Se consideraron los siguientes percentiles para asignar el nivel de ingresos:   

Nivel de Ingresos Alto: Se asignaron los casos desde percentil 60 en adelante. 

Nivel de Ingresos Medio: Se asignaron los casos entre el percentil 40 a 59. 

Nivel de Ingresos Bajo: Se asignaron los casos del percentil 40 hacia abajo. 

#### Desempeño modelos. 
Los modelos que predicen las variables de entrada presentan un Accuracy de 0.4353 en Edad mediante XGBoost, 0.6544 en Género y 0.4477 en Ocupación con RNN GRU.
La clasificación realizada por el modelo de nivel de ingreso seleccionado tiene una puntuación de Accuracy de 0.88 con el modelo de Extreme Gradient Boosting- XGBoost.

# Conclusiones <a name="conclusion"></a>

## Limitaciones

Dentro de las limitaciones más relevantes que se encontraron a la hora de realizar este trabajo se encuentran las siguientes:   

No existe en este momento, metodologías robustas e información de lenguaje natural procesado adecuados al idioma español. 

Para lograr obtener un buen desempeño, se deben usar algoritmos que tienen un alto costo computacional en el procesamiento de datos. 

La extracción de información no se encuentra disponible para su libre descarga, que garantice una base robusta y balanceada. 

El entrenamiento de la base de datos se creó para cuentas de usuarios reconocidos públicamente, por lo cual las variables usadas en el modelo están asignadas a criterios de experto, por cuánto puede existir un margen de error y desbalanceo de las clases. 

La estimación final del modelo de nivel de ingreso, aunque presenta un buen nivel en términos del desempeño y las métricas evaluadas, en el momento de la implementación recibirá como variables de entrada las predicciones de los modelos estimados para género, profesión y rangos de edad, los cuales reciben como única variable de entrada el texto, las cuales estarán afectadas por no presentar en todos los casos buenos niveles de precisión; de tal manera que, se puede afectar y distorsionar el resultado final de la predicción del nivel de ingreso que es la salida final de la ejecución secuencial de los modelos mencionados previamente y la que mayor tiene relevancia para este caso. 

## Recomendaciones 

Dentro de las recomendaciones más destacadas para trabajos futuros a realizar en la predicción de variables sociodemográficas y nivel de ingreso empleando redes sociales digitales, se exponen las siguientes: 

Los modelos estimados mediante ensambles de árboles – para este caso XGBoost – presentan medidas de desempeño similares o incluso más altas que los modelos estimados mediante redes neuronales, esto, siendo importante al momento de la implementación de los modelos en los desarrollos posteriores, no solo por las mejores métricas evaluadas, sino también por la eficiencia y el bajo costo en el uso de los recursos computacionales en la estimación y predicción de las categorías de interés.  

Robustecer los lexicones en el idioma español. 

Construir o implementar nuevas variables que puedan robustecer el desempeño de los modelos. 

Implementar los modelos bajo información de las demás redes sociales disponibles que permitan robustecer los resultados del caso de uso, mediante el uso de los demás componentes disponibles. 

En atención a una posterior etapa de este trabajo, en lo que se refiere la implementación del modelo se deber tener en cuenta que para cada variable (edad, genero, profesión) se aplica un modelo el cual tiene asociado un margen de error y que a su vez se usarían como entrada en el modelo para la predicción del nivel de ingreso.  
