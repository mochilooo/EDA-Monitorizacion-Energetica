# Hipótesis del proyecto EDA

## 1. Objetivo del análisis

Explorar las relaciones entre las condiciones ambientales interiores y el consumo energético residencial, identificando diferencias entre viviendas y entre los grupos UHI (Urban Heat Island) y UP (Urban Periphery).

El análisis tendrá un carácter exploratorio. Las relaciones estadísticas identificadas no se interpretarán como relaciones causales.

## 2. Hipótesis principales

### H01. Relación entre temperatura interior y consumo eléctrico

**Hipótesis:** existen asociaciones estadísticas entre la temperatura interior de las viviendas y su consumo eléctrico.

**Variables implicadas:**
- Temperatura interior.
- Consumo eléctrico.

**Análisis previsto:**
- Evolución temporal de ambas variables.
- Distribuciones y estadísticos descriptivos.
- Correlaciones.
- Comparaciones por vivienda.

**Limitaciones:** la asociación no demuestra que la temperatura interior determine el consumo eléctrico. Tampoco disponemos de información suficiente sobre los equipos eléctricos utilizados en cada vivienda.

### H02. Relación entre humedad interior y consumo energético

**Hipótesis:** existen diferencias o asociaciones entre los niveles de humedad relativa interior y los patrones de consumo energético de las viviendas.

**Variables implicadas:**
- Humedad relativa.
- Consumo eléctrico.
- Consumo de gas.

**Análisis previsto:**
- Distribución de la humedad.
- Comparación de patrones temporales.
- Análisis de correlaciones.

**Limitaciones:** una asociación estadística no permite establecer una relación causal entre humedad y consumo.

### H03. Diferencias entre los grupos UHI y UP

**Hipótesis:** existen diferencias en las condiciones ambientales interiores y en los patrones de consumo energético entre las viviendas de los grupos UHI y UP.

**Variables implicadas:**
- Grupo de vivienda (UHI o UP).
- Temperatura interior.
- Humedad relativa.
- Consumo eléctrico.
- Consumo de gas.

**Análisis previsto:**
- Comparación de distribuciones.
- Comparación de estadísticos descriptivos.
- Evolución temporal por grupo.
- Comparaciones utilizando periodos temporales equivalentes.

**Limitaciones:** las diferencias observadas no podrán atribuirse exclusivamente al efecto de isla de calor urbana. Pueden intervenir otras características de las viviendas y sus ocupantes que no están recogidas en el dataset.

### H04. Diferencias de comportamiento entre viviendas

**Hipótesis:** existen diferencias entre viviendas en sus patrones de consumo eléctrico y de gas, así como en sus condiciones ambientales interiores.

**Variables implicadas:**
- Identificador de vivienda.
- Temperatura interior.
- Humedad relativa.
- Consumo eléctrico.
- Consumo de gas.

**Análisis previsto:**
- Estadística descriptiva por vivienda.
- Comparación de distribuciones.
- Identificación de patrones y comportamientos diferenciados.
- Análisis de variabilidad entre viviendas.

**Limitaciones:** las diferencias observadas no permiten identificar por sí solas sus causas, ya que no disponemos de información completa sobre ocupación, superficie, aislamiento o hábitos de los residentes.

## 3. Análisis exploratorios complementarios

Además de las hipótesis principales, se estudiarán posibles patrones temporales:

- Diferencias entre periodos del año.
- Variaciones diarias y horarias del consumo.
- Evolución de la temperatura y humedad interiores.
- Posibles diferencias estacionales entre los grupos UHI y UP.

Estos análisis dependerán de la cobertura temporal y de la disponibilidad de registros comparables.

## 4. Variables disponibles y límites del estudio

El dataset permite estudiar:

| Variable | Disponibilidad |
|---|---|
| Temperatura interior | 20 viviendas |
| Humedad relativa interior | 20 viviendas |
| Consumo eléctrico | 19 viviendas |
| Consumo de gas | 20 viviendas |
| Grupo UHI/UP | 20 viviendas |
| Fecha y hora | Según cobertura de cada archivo |

No se han identificado en los archivos inspeccionados variables de temperatura exterior, meteorología, ocupación, superficie de vivienda o características constructivas.

Por tanto, no se formularán conclusiones que requieran esas variables sin incorporar previamente una fuente de datos adicional.

## 5. Estado de las hipótesis

Las hipótesis están formuladas como líneas de investigación pendientes de contraste.

No se considera confirmada ni rechazada ninguna hipótesis en esta fase.

La evaluación se realizará durante el análisis exploratorio, utilizando los datos disponibles y documentando las limitaciones de cada resultado.

## 6. Revisión de hipótesis

Las hipótesis podrán modificarse si durante el análisis se detectan problemas de calidad, limitaciones de cobertura o relaciones que requieran reformular las preguntas de investigación.

Cualquier modificación deberá justificarse y quedar registrada.

## 7. Consideraciones derivadas de la validación temporal

La validación temporal ha identificado diferencias de cobertura e interrupciones de distinta duración entre las series de las viviendas.

Por tanto:
- Las hipótesis se contrastarán utilizando únicamente las variables y periodos disponibles para cada análisis.
- Las comparaciones entre viviendas y entre grupos UHI y UP deberán utilizar ventanas temporales equivalentes o justificar expresamente las diferencias de cobertura.
- La existencia de interrupciones no implica por sí sola que una vivienda deba excluirse de todos los análisis.
- No se imputarán automáticamente los periodos sin registros para facilitar las comparaciones.

Estas consideraciones no modifican las hipótesis principales, pero condicionan la estrategia analítica y la interpretación de los resultados.
## 3. Prioridad y estrategia de contraste

Para mantener un alcance viable, las hipótesis se organizarán en dos niveles.

### Hipótesis prioritarias

**H01. Relación entre temperatura interior y consumo eléctrico**

Se estudiará mediante:
- Evolución diaria de temperatura y consumo eléctrico.
- Análisis de asociaciones entre ambas variables.
- Comparación de patrones entre viviendas.

**H02. Relación entre humedad interior y consumo energético**

Se estudiará mediante:
- Evolución diaria de humedad, electricidad y gas.
- Análisis de asociaciones entre las variables.
- Comparación de patrones entre viviendas.

**H03. Diferencias entre los grupos UHI y UP**

Se estudiará mediante:
- Comparación de temperatura y humedad interiores.
- Comparación de consumo eléctrico y de gas.
- Comparación de indicadores calculados por vivienda.
- Utilización de periodos temporales equivalentes cuando sea posible.

### Hipótesis complementaria

**H04. Diferencias de comportamiento entre viviendas**

Se estudiará mediante:
- Estadísticos descriptivos por vivienda.
- Comparación de distribuciones.
- Identificación de patrones diferenciados.

Su desarrollo dependerá del tiempo disponible y de los resultados obtenidos en los análisis prioritarios.

## 4. Estrategia de análisis temporal

Se utilizarán dos niveles de agregación:

- **Horario:** estudiar los patrones intradiarios y los perfiles de consumo.
- **Diario:** estudiar la evolución temporal y las asociaciones entre variables.

Para las variables energéticas se sumarán los registros de 15 minutos disponibles en cada periodo. Para temperatura y humedad se calcularán medias.

Los agregados deberán superar un criterio mínimo de cobertura. El umbral se establecerá durante la Fase 4, después de analizar la distribución real de registros completos e incompletos.

## 5. Unidad de análisis y comparaciones

La unidad de análisis dependerá de la pregunta:

- Los registros de 15 minutos se utilizarán para explorar la evolución temporal dentro de cada vivienda.
- Las viviendas serán la unidad de comparación para estudiar diferencias entre hogares.
- Las viviendas serán también la unidad estadística para comparar UHI y UP.

No se tratarán todos los registros temporales como observaciones independientes en las comparaciones entre grupos.

Las relaciones entre variables se estudiarán preferentemente a partir de agregados diarios por vivienda, teniendo en cuenta la dependencia temporal de las observaciones.

## 6. Alcance y exclusiones

El proyecto tendrá un enfoque exploratorio y se centrará en análisis descriptivos, temporales, de asociación y comparativos.

No se desarrollarán modelos predictivos ni se formularán conclusiones causales.

Tampoco se incorporarán datos meteorológicos externos ni se realizará un análisis exhaustivo individual de las veinte viviendas.

La comparación entre laborables y fines de semana se considera complementaria y se realizará únicamente si el tiempo disponible lo permite.

## 7. Estado de las hipótesis

Las cuatro hipótesis permanecen pendientes de contraste.

H01, H02 y H03 constituyen el núcleo del análisis. H04 se considera complementaria.

La prioridad asignada no implica que ninguna hipótesis esté confirmada o rechazada. Su evaluación dependerá de los resultados obtenidos durante las fases de análisis.