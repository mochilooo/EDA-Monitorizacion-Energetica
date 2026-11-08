# Registro de evidencias

## 1. Identificación de la fuente

**Dataset:** MODIF-HABIT  
**Repositorio:** Zenodo  
**DOI:** https://doi.org/10.5281/zenodo.20367908  
**Licencia:** Creative Commons Attribution 4.0 (CC BY 4.0)

El conjunto de datos procede de un proyecto de monitorización energética residencial desarrollado en Madrid.

La muestra está formada por 20 viviendas:
- 10 viviendas del grupo UHI (Urban Heat Island).
- 10 viviendas del grupo UP (Urban Periphery).

Las variables disponibles son:
- Temperatura interior.
- Humedad relativa interior.
- Consumo eléctrico.
- Consumo de gas.

La frecuencia nominal de registro indicada por la fuente es de 15 minutos.

## 2. Inventario y estructura

Se han identificado dos archivos ZIP originales:

| Archivo | CSV identificados |
|---|---:|
| MADRID UHI.zip | 59 |
| MADRID UP.zip | 60 |
| **Total** | **119** |

Se identificaron 20 viviendas y se comprobó la distribución de archivos por vivienda y variable.

La vivienda D11 no dispone de archivo de electricidad. Las otras 19 viviendas disponen de las cuatro variables.

Los archivos originales se conservan en `src/data/raw/` sin modificaciones.

## 3. Estructura de los archivos CSV

Se identificaron dos formatos de cabecera:

- Temperatura y humedad: fila de índice 12.
- Electricidad y gas: fila de índice 14.

Los archivos contienen metadatos y estadísticas generadas por el software de monitorización, además de los registros temporales.

El README de MODIF-HABIT indica que el software calcula estadísticas como promedio, mediana, máximo y mínimo para las variables ambientales y energéticas.

Por tanto, no se debe asumir que todos los valores exportados son lecturas directas de los sensores.

## 4. Validación estructural y temporal

Se inspeccionaron los 119 archivos CSV mediante Python y Pandas.

Resultados obtenidos:

- 3.479.361 filas con fecha y hora válidas contabilizadas en los archivos.
- 0 fechas inválidas detectadas.
- 0 valores no numéricos detectados en las columnas de medición.

El recuento corresponde a filas de los archivos originales con fecha y hora válidas. No debe interpretarse todavía como número de mediciones únicas, ya que no se ha completado una comprobación global de duplicados.

Se comprobó la frecuencia temporal y se identificaron interrupciones de distinta duración.

## 5. Cobertura temporal

Se analizó la coincidencia temporal de las cuatro variables para las 19 viviendas que disponen de electricidad.

Las 19 viviendas presentan timestamps comunes entre temperatura, humedad, electricidad y gas.

La cobertura media aritmética estimada fue del 93,01 %, calculada sobre las 19 viviendas.

Para cada vivienda se dividió el número de timestamps comunes entre el número de timestamps esperados entre el primer y el último registro, tomando como referencia la frecuencia nominal de 15 minutos.

El cálculo no incluye D11 y no está ponderado por el número de registros o la duración de cada vivienda.

Esta cifra es una estimación de cobertura temporal, no una medida global de calidad del dataset. Se detectaron interrupciones importantes en algunas viviendas.

## 6. Disponibilidad de variables

Se identificaron las siguientes condiciones:

- 20 viviendas disponen de temperatura, humedad y gas.
- 19 viviendas disponen de electricidad.
- D11 no dispone de mediciones eléctricas.

Se conservará D11 para los análisis que no requieran electricidad. No se imputarán datos eléctricos inexistentes.

## 7. Incidencias en los registros energéticos

Durante la inspección se identificaron 42 registros negativos:

- 26 correspondientes a electricidad.
- 16 correspondientes a gas.
- Distribuidos en 16 timestamps diferentes.

Se observaron coincidencias temporales de valores negativos entre distintas viviendas y variables.

La documentación técnica identifica los equipos PowerSense para electricidad y GasSens para gas, pero no explica el origen de estos valores ni la semántica exacta de cada registro energético.

Por tanto, no se puede determinar todavía si corresponden a errores de medición, procesamiento, exportación u otra circunstancia.

Los valores originales se conservarán sin sustituirlos por cero ni eliminarlos.

## 8. Documentación técnica de los equipos

La tabla técnica de MODIF-HABIT identifica los siguientes dispositivos:

| Equipo | Función |
|---|---|
| EnergoBox Gateway | Adquisición y comunicación de datos |
| Energovision | Visualización y medición de temperatura y humedad |
| PowerSense (80 A) | Medición eléctrica mediante sensores de corriente |
| GasSens | Medición de gas mediante contador de impulsos |
| Energy Control | Plataforma de visualización y análisis |

Los sensores ambientales están integrados en una pantalla situada en el salón de cada vivienda, a una altura aproximada de 1,2–1,7 metros.

La documentación indica que los equipos venían calibrados de fábrica.

## 9. Limitaciones identificadas

1. Diferencias de cobertura temporal entre viviendas y variables.
2. Interrupciones de distinta duración en las series temporales; 45 de 79 series presentan al menos un intervalo superior a 24 horas.
3. Ausencia de electricidad en D11.
4. Presencia de 42 registros energéticos negativos sin explicación documental.
5. Falta de información suficiente para determinar la semántica exacta de cada registro energético.
6. Las mediciones ambientales corresponden al punto de instalación del dispositivo en el salón, no a una medición de todas las habitaciones.
7. Ausencia de información explícita sobre zona horaria y desplazamiento UTC, que limita la interpretación de algunas marcas temporales repetidas.

## 10. Conclusión de la validación

La inspección ha permitido identificar la procedencia, estructura, variables disponibles y principales características temporales del conjunto de datos.

El dataset presenta condiciones suficientes para continuar con el desarrollo metodológico del proyecto, siempre que las limitaciones identificadas se tengan en cuenta durante la integración, limpieza y análisis.

La validación definitiva de esta fase queda condicionada a la revisión de los criterios de aceptación y a la trazabilidad de los resultados en el Notebook.

### E09. Duplicados y alineación temporal

**Objetivo:** comprobar la existencia de registros duplicados y verificar la alineación temporal de las mediciones.

**Resultados obtenidos:**

- Se analizaron los 119 archivos CSV.
- Se detectaron duplicados internos en 77 archivos.
- Estos duplicados afectan a 848 filas, correspondientes a 424 marcas temporales repetidas.
- Al agrupar los registros por vivienda y variable se identificaron 462 registros duplicados excedentes:
  - 424 duplicados internos.
  - 38 duplicados adicionales por solapamientos entre archivos consecutivos.
- Los 38 solapamientos corresponden a registros de temperatura y humedad del 31/12/2019.
- Se compararon los valores de ambos archivos en los 38 casos y se comprobó que coinciden exactamente.
- Los registros analizados están alineados con la cuadrícula temporal nominal de 15 minutos.

**Interpretación:**

Los solapamientos entre archivos consecutivos parecen responder a la inclusión de una misma marca temporal en los límites de los archivos. Al coincidir exactamente sus valores, podrán consolidarse durante la integración, conservando una única observación y dejando constancia de la operación.

Los duplicados internos requieren un análisis específico antes de eliminarlos. Los archivos no incluyen información de zona horaria ni desplazamiento UTC, por lo que todavía no se puede determinar con certeza el origen de todas las marcas temporales repetidas.

**Conclusión:**

Se ha identificado y cuantificado la duplicidad temporal. No se modificarán los archivos originales. El tratamiento se realizará posteriormente durante la integración y limpieza de los datos.

### E10. Continuidad temporal de las series

**Objetivo:** analizar la continuidad de las series temporales completas por vivienda y variable, evitando limitar la comprobación a cada archivo CSV por separado.

**Resultados obtenidos:**

- Se analizaron 79 series temporales: 19 viviendas con cuatro variables y la vivienda D11 con tres variables.
- 45 de las 79 series presentan al menos un intervalo superior a 24 horas.
- 24 de las 79 series presentan al menos un intervalo superior a 7 días.
- 7 de las 79 series presentan al menos un intervalo superior a 30 días.
- En D01 se identificó un intervalo máximo de 97 días, 22 horas y 15 minutos en electricidad, humedad y temperatura.
- En D18 se identificó un intervalo máximo de 60 días, 15 horas y 15 minutos en electricidad y gas.

**Principales intervalos identificados:**

| Vivienda | Variable | Último registro anterior | Primer registro posterior | Duración |
|---|---|---|---|---|
| D01 | Electricidad | 01/08/2019 19:45 | 07/11/2019 18:00 | 97 días, 22 h y 15 min |
| D01 | Humedad | 01/08/2019 20:00 | 07/11/2019 18:15 | 97 días, 22 h y 15 min |
| D01 | Temperatura | 01/08/2019 20:00 | 07/11/2019 18:15 | 97 días, 22 h y 15 min |
| D18 | Electricidad | 06/08/2020 05:45 | 05/10/2020 21:00 | 60 días, 15 h y 15 min |
| D18 | Gas | 06/08/2020 05:45 | 05/10/2020 21:00 | 60 días, 15 h y 15 min |

**Interpretación:**

Los recuentos por umbral indican el número de series que presentan al menos un intervalo superior al límite indicado. No representan porcentajes de mediciones perdidas ni porcentajes de cobertura.

La coincidencia de interrupciones en varias variables de una misma vivienda es compatible con incidencias comunes de monitorización, pero la información disponible no permite determinar su causa. No se atribuyen automáticamente a fallos de equipos, cortes de comunicación u otras circunstancias concretas.

La diferencia entre los resultados preliminares por archivo y los resultados consolidados por vivienda y variable se debe a que una interrupción puede quedar repartida entre dos archivos consecutivos. Por ello, la continuidad global debe evaluarse después de combinar temporalmente los registros de todos los archivos correspondientes a cada serie.

**Conclusión:**

La continuidad temporal es heterogénea entre viviendas y variables. Los intervalos largos deberán tenerse en cuenta al seleccionar ventanas temporales comparables para los análisis posteriores. No se eliminarán viviendas ni se imputarán periodos automáticamente por la existencia de estas interrupciones.
