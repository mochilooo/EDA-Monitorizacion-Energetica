# Decisiones metodológicas

## 1. Objetivo

Registrar las decisiones metodológicas adoptadas durante la obtención, inspección y validación del conjunto de datos MODIF-HABIT.

Cada decisión incluye su justificación y, cuando corresponde, las limitaciones que deben tenerse en cuenta durante las siguientes fases del proyecto.

## 2. Decisiones adoptadas

### DM01. Conservación de los archivos originales

**Decisión:** mantener los archivos ZIP originales sin modificaciones en `src/data/raw/`.

**Justificación:** preservar la integridad de la fuente y permitir reproducir los procesos de transformación posteriores.

**Estado:** adoptada.

### DM02. Lectura de los CSV mediante identificación de cabeceras

**Decisión:** utilizar procedimientos de lectura diferenciados según el tipo de variable.

- Temperatura y humedad: cabecera en la fila de índice 12.
- Electricidad y gas: cabecera en la fila de índice 14.

**Justificación:** los archivos contienen metadatos antes de la tabla de mediciones y no pueden leerse correctamente utilizando directamente la primera fila como cabecera.

**Estado:** adoptada.

### DM03. Conservación de D11

**Decisión:** conservar la vivienda D11 en el conjunto de datos.

**Justificación:** dispone de temperatura, humedad y gas, aunque carece de registros de electricidad.

**Aplicación:** D11 podrá utilizarse en análisis que no requieran la variable eléctrica. Se excluirá únicamente de los análisis que necesiten esa variable.

**Estado:** adoptada.

### DM04. Tratamiento de los registros energéticos negativos

**Decisión:** conservar los 42 registros negativos identificados, sin sustituirlos por cero ni eliminarlos automáticamente.

**Justificación:** la documentación técnica disponible no explica su origen ni permite clasificarlos como errores confirmados.

**Aplicación:** deberán identificarse y analizarse durante la fase de limpieza y control de calidad.

**Estado:** adoptada provisionalmente.

### DM05. Tratamiento de los valores cero

**Decisión:** no considerar automáticamente los valores cero como datos ausentes o erróneos.

**Justificación:** especialmente en el consumo de gas, un valor cero puede representar un periodo sin consumo.

**Aplicación:** se conservarán inicialmente y se estudiará su distribución y significado antes de aplicar cualquier transformación.

**Estado:** adoptada provisionalmente.

### DM06. Tratamiento de las interrupciones temporales

**Decisión:** no eliminar automáticamente viviendas o periodos por presentar interrupciones en sus series temporales.

**Justificación:** las viviendas presentan diferentes niveles de cobertura y duración de las interrupciones. Una exclusión general podría reducir innecesariamente la muestra.

**Aplicación:** documentar la cobertura individual y seleccionar los periodos adecuados según cada análisis.

**Estado:** adoptada.

### DM07. Comparación entre viviendas

**Decisión:** considerar las diferencias de cobertura temporal y disponibilidad de variables antes de realizar comparaciones entre viviendas o grupos.

**Justificación:** las viviendas no presentan necesariamente los mismos periodos de observación ni la misma cantidad de registros.

**Aplicación:** definir ventanas temporales comparables para cada análisis y documentar los criterios de selección.

**Estado:** adoptada.

### DM08. Interpretación de las mediciones ambientales

**Decisión:** interpretar temperatura y humedad como mediciones realizadas en el punto de instalación del dispositivo, situado en el salón.

**Justificación:** la documentación técnica describe sensores integrados en la pantalla Energovision instalada en esa estancia.

**Aplicación:** no generalizar los valores como representativos de todas las habitaciones de la vivienda.

**Estado:** adoptada.

### DM09. Interpretación de los registros energéticos

**Decisión:** no asumir todavía que cada registro energético representa exactamente el consumo producido durante los 15 minutos anteriores.

**Justificación:** aunque la frecuencia nominal es de 15 minutos, la documentación consultada no define suficientemente la semántica temporal de cada registro ni el procedimiento de agregación.

**Aplicación:** mantener esta cuestión abierta hasta disponer de información suficiente.

**Estado:** pendiente de aclaración.

## 3. Criterios generales para las siguientes fases

Durante el preprocesamiento y la limpieza se aplicarán los siguientes principios:

1. No eliminar registros sin una justificación documentada.
2. No sustituir valores negativos o cero de forma automática.
3. Investigar los valores ausentes antes de decidir su tratamiento.
4. Diferenciar errores confirmados de valores atípicos.
5. No eliminar valores extremos únicamente por su magnitud.
6. Conservar la trazabilidad de las transformaciones realizadas.
7. Documentar las exclusiones de viviendas, variables o periodos.
8. Evitar interpretar correlaciones como relaciones causales.

## 4. Cuestiones pendientes

- Aclarar la semántica exacta de los registros energéticos.
- Investigar el origen de los valores negativos.
- Determinar los criterios de selección de ventanas temporales comparables.
- Definir el tratamiento de las interrupciones según el análisis que se realice.
- Establecer los criterios definitivos de limpieza antes de modificar los datos.

## 5. Control de cambios

Las decisiones podrán revisarse si aparecen nuevas evidencias durante el desarrollo del proyecto.

Cualquier modificación deberá incluir su justificación y el impacto que tenga sobre los análisis realizados.

### DM10. Tratamiento de solapamientos entre archivos

Se han identificado 38 marcas temporales duplicadas entre archivos consecutivos de temperatura y humedad. Todos los casos corresponden al 31/12/2019 y presentan valores idénticos.

**Decisión:** durante la integración se conservará una única observación por vivienda, variable y marca temporal en estos casos. Se registrará la operación para mantener la trazabilidad.

Los archivos originales permanecerán intactos.

### DM11. Tratamiento de duplicados internos y marcas temporales repetidas

Se han detectado 424 marcas temporales repetidas dentro de los archivos originales. Todavía no se ha determinado con certeza su origen.

**Decisión:** no se eliminarán automáticamente. Antes de decidir su tratamiento, se investigará si están relacionadas con cambios horarios u otras circunstancias del sistema de adquisición.

La ausencia de información explícita sobre zona horaria y desplazamiento UTC limita la interpretación de estas marcas temporales.

### DM12. Evaluación de la continuidad por serie temporal completa

**Decisión:** evaluar las interrupciones temporales agrupando todos los archivos de cada vivienda y variable, ordenando las marcas temporales y eliminando únicamente las repeticiones para el cálculo de los intervalos de continuidad. Esta operación de cálculo no implica eliminar duplicados del conjunto de datos integrado.

**Justificación:** la comprobación individual de cada CSV puede no detectar interrupciones que se extienden entre dos archivos consecutivos. El análisis consolidado permite evaluar la continuidad real de cada serie temporal.

**Resultados de referencia:**
- Se analizaron 79 series temporales.
- 45 presentan al menos un intervalo superior a 24 horas.
- 24 presentan al menos un intervalo superior a 7 días.
- 7 presentan al menos un intervalo superior a 30 días.
- D01 presenta intervalos máximos de 97 días, 22 horas y 15 minutos en electricidad, humedad y temperatura.
- D18 presenta intervalos máximos de 60 días, 15 horas y 15 minutos en electricidad y gas.

**Aplicación:** documentar los intervalos y tenerlos en cuenta al definir ventanas temporales comparables. No eliminar viviendas ni imputar automáticamente los periodos sin registros.

**Estado:** adoptada para la evaluación de continuidad; el tratamiento de los periodos sin registros queda pendiente de cada análisis.

### DM12. Interpretación operativa de los registros energéticos

**Decisión:** para los análisis horarios y diarios se tratarán los valores de electricidad y gas como cantidades de energía expresadas en kWh y se sumarán los registros de 15 minutos disponibles dentro de cada periodo.

**Justificación:** los archivos originales identifican estas variables como datos de energía de frecuencia *Quarter Hourly* y expresan sus valores en kWh. La documentación del dataset establece una resolución temporal de 15 minutos.

**Limitación:** esta interpretación permite realizar una agregación operativa coherente, pero no demuestra por sí sola el intervalo físico exacto al que corresponde cada valor. Se mantendrá esta limitación documentada.

**Aplicación:**
- Energía eléctrica y gas: suma de los registros para obtener energía horaria y diaria.
- Temperatura y humedad: cálculo de medias horarias y diarias.

**Estado:** adoptada como criterio operativo.

### DM13. Tratamiento de las filas de resumen de los CSV

**Decisión:** excluir del conjunto de mediciones las filas iniciales que contienen estadísticas globales del archivo, como total, promedio, mediana, máximo y mínimo.

**Justificación:** estas filas son metadatos estadísticos del archivo y no observaciones temporales individuales.

**Aplicación:** la lectura de cada CSV deberá comenzar en la cabecera correspondiente a su tipo de variable.

**Estado:** adoptada.

### DM14. Agregación temporal para el análisis

**Decisión:** trabajar con dos niveles temporales principales:
- Horario, para estudiar patrones intradiarios.
- Diario, para estudiar evolución temporal y relaciones entre variables.

**Aplicación:**
- Electricidad y gas: suma de los valores disponibles en cada hora o día.
- Temperatura y humedad: media de los valores disponibles en cada hora o día.

**Limitación:** las agregaciones deberán tener en cuenta la existencia de interrupciones y periodos incompletos.

**Estado:** adoptada.

### DM15. Tratamiento de periodos incompletos

**Decisión:** no completar automáticamente los intervalos ausentes con valores cero ni calcular agregaciones como si todos los periodos estuvieran completos.

**Aplicación:** durante la Fase 4 se estudiará la completitud de las horas y los días. A partir de esa información se establecerá un umbral mínimo de cobertura para aceptar cada agregado.

**Estado:** adoptada; umbral pendiente de definir en Fase 4.

### DM16. Unidad de análisis para las comparaciones

**Decisión:** distinguir la unidad de análisis según el objetivo:

- Registro de 15 minutos: exploración de la evolución temporal dentro de cada vivienda.
- Vivienda: comparación de patrones entre hogares.
- Vivienda: unidad estadística para las comparaciones entre los grupos UHI y UP.

**Justificación:** los registros de una misma vivienda están temporalmente relacionados y no deben tratarse como observaciones independientes en las comparaciones entre grupos.

**Aplicación:** las comparaciones UHI-UP se basarán en indicadores calculados por vivienda, evitando considerar millones de registros temporales como si fueran millones de viviendas independientes.

**Estado:** adoptada.

### DM17. Alcance del análisis

**Decisión:** limitar el proyecto a análisis descriptivos, temporales, de asociación y comparativos.

Quedan fuera del alcance:
- Modelos predictivos.
- Interpretaciones causales.
- Incorporación de datos meteorológicos externos.
- Análisis exhaustivo individual de todas las viviendas.

El análisis de laborables frente a fines de semana se considera complementario y podrá omitirse si el tiempo disponible no permite desarrollarlo adecuadamente.

**Justificación:** mantener un alcance viable y coherente con el objetivo exploratorio y el tiempo disponible para la presentación.

**Estado:** adoptada.