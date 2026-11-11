# Estado de las fases del proyecto EDA

## Información general

**Proyecto:** Monitorización energética residencial MODIF-HABIT.

**Objetivo:** explorar las relaciones entre las condiciones ambientales interiores y el consumo energético de las viviendas, identificando diferencias entre hogares y entre los grupos UHI y UP.

**Estado general:** EN DESARROLLO.

---

## Fase 1. Selección temática y definición del problema

**Estado:** VALIDADA

### Trabajo realizado
- Selección de la monitorización energética residencial como temática.
- Identificación del conjunto de datos MODIF-HABIT.
- Definición de una pregunta de investigación provisional.
- Identificación del objetivo general del proyecto.

### Evidencias
- Fuente de datos identificada.
- DOI y documentación del dataset disponibles.
- Objetivo y temática incorporados al Notebook.

---

## FASE 2. Obtención y validación de datos

**Estado: VALIDADA**

### Trabajo realizado

- Identificación de MODIF-HABIT como fuente principal.
- Comprobación de la procedencia, autores y referencia bibliográfica.
- Verificación del DOI y de la licencia CC BY 4.0.
- Descarga y conservación de los dos archivos ZIP originales.
- Inventario de los 119 archivos CSV correspondientes a 20 viviendas.
- Identificación de las variables: temperatura, humedad, electricidad y gas.
- Inspección de cabeceras, estructura y formatos de los archivos.
- Validación global de fechas y valores numéricos.
- Análisis de cobertura temporal y disponibilidad de variables por vivienda.
- Identificación de D11 como vivienda sin registros de electricidad.
- Comprobación de coincidencias temporales entre las cuatro variables en 19 viviendas.
- Cuantificación de duplicados internos y solapamientos entre archivos.
- Verificación de que los 38 solapamientos entre archivos contienen valores idénticos.
- Revisión de la documentación técnica de los equipos de monitorización.

### Resultados principales

- 20 viviendas monitorizadas.
- 19 viviendas con las cuatro variables.
- 1 vivienda (D11) sin electricidad.
- 119 archivos CSV.
- 3.479.361 filas con fecha y hora válidas contabilizadas.
- 0 fechas inválidas detectadas.
- 0 valores no numéricos detectados.
- Cobertura temporal estimada media del 93,01 % en las 19 viviendas con las cuatro variables.
- 424 marcas temporales repetidas dentro de archivos.
- 38 solapamientos entre archivos consecutivos, con valores idénticos.
- 462 registros duplicados excedentes al agrupar por vivienda y variable.

### Limitaciones identificadas

- Diferencias de cobertura temporal entre viviendas y variables.
- Ausencia de electricidad en D11.
- Existencia de registros duplicados cuya causa todavía debe investigarse.
- Ausencia de información explícita sobre zona horaria y desplazamiento UTC.
- Valores negativos en algunas variables energéticas cuya semántica no está aclarada.
- Diferencias entre los periodos declarados en la documentación y los observados en determinados archivos.

### Tareas pendientes

- Revisar la coherencia final entre el Notebook y los documentos metodológicos.
- Confirmar que las evidencias y decisiones están correctamente registradas.
- Mantener documentadas las limitaciones que deberán tratarse en las fases de integración y limpieza.

### Criterio de cierre

La Fase 2 podrá validarse cuando la procedencia, licencia, estructura, disponibilidad, documentación y adecuación del dataset estén suficientemente verificadas, y sus limitaciones estén identificadas y documentadas.

La resolución definitiva de los valores negativos y de los duplicados internos se abordará en las fases posteriores, sin alterar los datos originales.

---

## Fase 3. Hipótesis y estrategia analítica

**Estado:** EN CURSO

### Trabajo realizado
- Definición de cuatro hipótesis principales.
- Identificación de las variables necesarias.
- Identificación de las principales limitaciones del conjunto de datos.
- Propuesta de análisis descriptivos, temporales y comparativos.

### Evidencias
- `documentation/hipotesis.md`.

### Pendiente
- Revisar la viabilidad de cada hipótesis.
- Definir los métodos estadísticos adecuados.
- Establecer los criterios de comparación entre viviendas y grupos.
- Definir las ventanas temporales que permitan comparaciones válidas.

### Criterio de cierre
Las hipótesis y la estrategia analítica deberán estar definidas, justificadas y ser compatibles con las variables y la calidad de los datos disponibles.

---

## Fase 4. Preprocesamiento e integración

**Estado:** NO INICIADA

### Trabajo previsto
- Diseñar el proceso de lectura de todos los CSV.
- Normalizar nombres de variables y formatos.
- Integrar las mediciones por vivienda y fecha.
- Comprobar la alineación temporal.
- Generar un conjunto de datos estructurado para el análisis.

### Criterio de cierre
Disponer de un conjunto integrado, reproducible y trazable, con las variables correctamente identificadas y las incidencias documentadas.

---

## Fase 5. Limpieza y control de calidad

**Estado:** NO INICIADA

### Trabajo previsto
- Investigar valores ausentes.
- Revisar valores negativos y extremos.
- Analizar duplicados.
- Estudiar interrupciones temporales.
- Aplicar las transformaciones justificadas.
- Documentar las exclusiones y modificaciones.

### Criterio de cierre
Disponer de datos preparados para el análisis, con todas las decisiones de limpieza justificadas y reproducibles.

---

## Fase 6. Análisis exploratorio de datos (EDA)

**Estado:** NO INICIADA

### Trabajo previsto
- Análisis descriptivo univariante.
- Análisis bivariante.
- Distribuciones y variabilidad.
- Evolución temporal.
- Comparaciones entre viviendas.
- Comparaciones entre grupos UHI y UP.
- Visualizaciones e interpretación de resultados.

### Criterio de cierre
Responder a las preguntas de investigación mediante resultados estadísticos y visualizaciones correctamente interpretadas.

---

## Fase 7. Verificación de hipótesis y conclusiones

**Estado:** NO INICIADA

### Trabajo previsto
- Contrastar las hipótesis formuladas.
- Interpretar los resultados.
- Identificar relaciones y diferencias relevantes.
- Exponer limitaciones.
- Formular conclusiones respaldadas por los datos.

### Criterio de cierre
Cada hipótesis deberá quedar evaluada y las conclusiones deberán estar justificadas por evidencias del análisis.

---

## Fase 8. Documentación, repositorio y presentación

**Estado:** NO INICIADA

### Trabajo previsto
- Revisar el Notebook completo.
- Actualizar el README.
- Organizar documentación y código.
- Comprobar la reproducibilidad.
- Preparar la memoria del proyecto.
- Preparar la presentación final de 15 minutos.

### Criterio de cierre
Entregar un proyecto reproducible, documentado y coherente con los resultados presentados.

---

## Registro de modificaciones
| 08/11/2026 | Fase 2 | Fase 2 validada tras documentar procedencia, estructura, disponibilidad, calidad inicial y limitaciones del dataset. El tratamiento de duplicados internos, valores negativos e interrupciones pendientes se abordará en fases posteriores. |

| Fecha | Fase | Modificación |
|---|---|---|
| 08/11/2026 | Fases 1–3 | Documentación inicial del estado y planificación del proyecto |

## Criterios generales de validación

Una fase no se considerará validada únicamente por haber ejecutado las tareas previstas.

Para validar cada fase será necesario:

1. Disponer de evidencias verificables.
2. Cumplir los criterios de cierre establecidos.
3. Documentar las decisiones metodológicas.
4. Identificar las limitaciones pendientes.
5. Comprobar la coherencia con las fases anteriores.

## Fase 3. Hipótesis y estrategia analítica

**Estado:** VALIDADA

### Trabajo realizado

- Definición de cuatro hipótesis de investigación.
- Priorización de H01, H02 y H03.
- Clasificación de H04 como hipótesis complementaria.
- Definición del enfoque descriptivo, temporal, relacional y comparativo.
- Definición de las agregaciones horarias y diarias.
- Definición de la unidad de análisis para cada tipo de comparación.
- Identificación de las limitaciones metodológicas que condicionarán el análisis.
- Delimitación del alcance para mantener el proyecto viable.

### Estrategia adoptada

- Análisis descriptivo de las cuatro variables principales.
- Evolución temporal horaria y diaria.
- Estudio de asociaciones entre variables ambientales y energéticas.
- Comparación entre viviendas.
- Comparación entre los grupos UHI y UP.
- Análisis de laborables frente a fines de semana como complemento opcional.

### Criterios metodológicos establecidos

- Sumar los registros energéticos para obtener energía horaria y diaria.
- Calcular medias horarias y diarias para temperatura y humedad.
- No completar huecos temporales con ceros.
- No tratar registros de 15 minutos como observaciones independientes en comparaciones entre viviendas o grupos.
- Utilizar la vivienda como unidad estadística para las comparaciones UHI-UP.
- No formular conclusiones causales ni desarrollar modelos predictivos.

### Limitaciones pendientes para fases posteriores

- Determinar el umbral de cobertura mínimo para aceptar agregaciones horarias y diarias.
- Investigar los valores negativos de electricidad y gas.
- Investigar los duplicados internos.
- Estudiar las interrupciones temporales.
- Establecer las ventanas temporales comparables entre viviendas y grupos.

### Evidencias

- `documentation/hipotesis.md`
- `documentation/decisiones_metodologicas.md`
- `documentation/registro_evidencias.md`
- Notebook `main.ipynb`

### Criterio de cierre

Las hipótesis y la estrategia analítica están definidas, justificadas y son compatibles con las variables y limitaciones identificadas en el conjunto de datos.

La resolución de las incidencias de calidad y la implementación de las transformaciones se abordarán en las fases posteriores.

---

## Fase 4. Preprocesamiento e integración

**Estado:** NO INICIADA

### Trabajo previsto

- Diseñar el proceso de lectura de todos los CSV.
- Excluir las filas iniciales de estadísticas resumen.
- Normalizar nombres de variables y formatos.
- Integrar las mediciones por vivienda y fecha.
- Comprobar la alineación temporal.
- Construir las agregaciones horarias y diarias.
- Analizar la completitud de los periodos.
- Proponer un umbral de cobertura para aceptar agregaciones.

### Criterio de cierre

Disponer de un conjunto integrado, reproducible y trazable, con las variables correctamente identificadas y las incidencias documentadas.
# Actualización de revisión integral

**Fecha:** 09/11/2026  
**Estado global:** VALIDADA para el alcance exploratorio descrito.

La revisión final incorporó un umbral de 72 registros diarios por variable para las asociaciones y comparaciones entre viviendas, actualizó la memoria y la presentación, y dejó constancia de las comprobaciones en `validacion_final.md`. La copia original se conserva dentro de la entrega. Las limitaciones sobre causalidad, cobertura y variables no observadas permanecen vigentes.

