# Monitorización inteligente del consumo energético residencial

**Proyecto de Data Science · Análisis Exploratorio de Datos (EDA)**

## 1. Descripción

Este proyecto desarrolla un análisis exploratorio de datos de monitorización energética residencial. Se estudian las condiciones ambientales interiores y los consumos de electricidad y gas de 20 viviendas de Madrid, pertenecientes a dos grupos: UHI (*Urban Heat Island*) y UP (*Urban Periphery*).

El análisis busca identificar patrones temporales, asociaciones entre variables y diferencias entre grupos y viviendas individuales. El enfoque es descriptivo: los resultados no permiten establecer causalidad.

## 2. Objetivos

- Describir las variables ambientales y energéticas disponibles.
- Explorar la evolución diaria y los perfiles horarios de consumo.
- Estudiar la asociación entre temperatura interior y consumo energético.
- Estudiar la asociación entre humedad interior y consumo energético.
- Comparar descriptivamente las viviendas de los grupos UHI y UP.
- Examinar la variabilidad entre viviendas individuales.

## 3. Hipótesis de trabajo

| Hipótesis | Pregunta de análisis | Estrategia |
|---|---|---|
| **H01** | ¿Cómo se relaciona la temperatura interior con el consumo de electricidad y gas? | Correlación de Spearman por vivienda, con datos diarios emparejados. |
| **H02** | ¿Cómo se relaciona la humedad interior con el consumo de electricidad y gas? | Correlación de Spearman por vivienda, con datos diarios emparejados. |
| **H03** | ¿Existen diferencias en las condiciones interiores y el consumo energético entre UHI y UP? | Indicadores medios por vivienda y comparación mediante boxplots. |
| **H04** | ¿Qué variabilidad existe entre viviendas individuales? | Comparación de medias, mínimos, máximos y desviaciones estándar por vivienda. |

H01 y H02 estudian asociaciones entre variables. H03 y H04 describen diferencias entre grupos y hogares. No se plantean como pruebas causales.

## 4. Fuente y características de los datos

**Dataset:** MODIF-HABIT  
**Procedencia:** viviendas residenciales de Madrid, España.  
**Repositorio:** [https://doi.org/10.5281/zenodo.20367908](https://doi.org/10.5281/zenodo.20367908)  
**Licencia indicada en el README inicial:** CC BY 4.0 (consultar la ficha del repositorio para las condiciones aplicables).

| Característica | Descripción |
|---|---|
| Viviendas | 20: 10 UHI y 10 UP |
| Variables | Temperatura interior, humedad relativa, electricidad y gas |
| Frecuencia nominal | 15 minutos |
| Archivos originales | 119 CSV: 59 UHI y 60 UP |
| Periodo observado global | 16/05/2019 11:30 – 08/02/2021 18:30 |
| Registros con fecha y hora válidas | 3.479.361 |
| Tabla integrada | 1.075.812 filas y 11 columnas |

Unidades identificadas en los CSV inspeccionados:

- Temperatura: °C.
- Humedad relativa: %.
- Electricidad: kWh.
- Gas: kWh.

La vivienda D11 no dispone de archivo de electricidad. No se inventa ni se imputa ese consumo.

## 5. Estructura del repositorio

La estructura documentada a partir del notebook y del README de trabajo es:

```text
EDA-Monitorizacion-Energetica/
├── README.md
├── .gitignore
├── documentation/
├── src/
│   ├── main.ipynb
│   └── data/
│       └── raw/
│           ├── MADRID UHI.zip
│           └── MADRID UP.zip
└── data/
    └── processed/
        └── madrid_energy_integrated.csv
```

El notebook utiliza rutas relativas desde `src/`: lee los ZIP desde `src/data/raw/` y guarda la tabla integrada en `data/processed/` en la raíz del proyecto. Si la estructura local difiere, deben ajustarse las rutas del notebook.

## 6. Metodología y procesamiento

1. Inventario de los CSV incluidos en los ZIP UHI y UP.
2. Inspección de la estructura de los archivos y de sus metadatos.
3. Lectura de los registros temporales, distinguiendo encabezados ambientales y energéticos.
4. Identificación de grupo, vivienda, variable y archivo de origen.
5. Conversión de fecha y hora a una marca temporal.
6. Integración por grupo, vivienda y fecha/hora.
7. Consolidación de registros duplicados mediante la media, conservando el número de registros originales.
8. Control de calidad: ausencias, duplicados, valores negativos y cobertura temporal.
9. Agregación diaria y horaria para el análisis exploratorio.
10. Correlaciones Spearman por vivienda y comparación descriptiva de indicadores entre hogares.

### Decisiones de calidad de datos

- Los registros ausentes se mantienen como ausentes; no se sustituyen por cero.
- Se identificaron 462 combinaciones duplicadas en el conjunto largo: 268 con valores idénticos y 194 con valores diferentes. En la integración se consolidaron mediante la media y se conservó el recuento de registros.
- La tabla integrada no presenta claves duplicadas por grupo, vivienda y fecha/hora.
- Se identificaron 26 valores negativos de electricidad y 16 de gas. Se conservaron para revisión porque su origen no está determinado.
- La cobertura temporal es desigual. En 79 series temporales consolidadas, 45 presentan al menos una interrupción superior a 24 horas, 24 superior a 7 días y 7 superior a 30 días.
- No se dispone de información suficiente sobre la zona horaria de los archivos.

## 7. Resultados principales

### H01 · Temperatura y consumo

Mediana de las correlaciones Spearman calculadas por vivienda:

- Temperatura–electricidad: **−0,141** (19 viviendas con resultado).
- Temperatura–gas: **−0,703** (20 viviendas).

La asociación negativa es más marcada para el gas. Para electricidad es débil y heterogénea. El resultado no demuestra causalidad y puede estar condicionado por la estacionalidad.

### H02 · Humedad y consumo

- Humedad–electricidad: **+0,165** (19 viviendas con resultado).
- Humedad–gas: **+0,396** (20 viviendas).

Las asociaciones son positivas en el resumen por vivienda, más visibles para gas, aunque varían entre hogares.

### H03 · Comparación UHI y UP

Las medianas por grupo muestran:

- Temperatura: UHI 23,68 °C; UP 23,74 °C.
- Humedad: UHI 44,45 %; UP 39,04 %.
- Electricidad: UHI 6,62; UP 6,19.
- Gas: UHI 15,27; UP 11,87.

La diferencia descriptiva más visible aparece en humedad y gas. No se han realizado pruebas de significación estadística.

### H04 · Variabilidad entre viviendas

Resumen de indicadores medios por vivienda:

| Variable | Mínimo | Máximo | Media | Desv. estándar |
|---|---:|---:|---:|---:|
| Temperatura (°C) | 21,16 | 25,27 | 23,63 | 1,05 |
| Humedad (%) | 34,93 | 50,72 | 41,95 | 4,80 |
| Electricidad (kWh/día) | 2,26 | 13,89 | 7,18 | 3,11 |
| Gas (kWh/día) | 0,16 | 38,60 | 15,15 | 12,03 |

La variabilidad entre viviendas es especialmente elevada para el gas.

## 8. Herramientas

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- SciPy (`scipy.stats.spearmanr`)

## 9. Ejecución

1. Clonar o descargar el repositorio.
2. Mantener los ZIP originales en `src/data/raw/`.
3. Abrir una terminal en la carpeta `src/`.
4. Instalar las librerías utilizadas:

```bash
python -m pip install pandas numpy matplotlib scipy jupyter
```

5. Iniciar Jupyter:

```bash
jupyter notebook
```

6. Abrir y ejecutar `main.ipynb` de principio a fin.

El notebook utiliza rutas relativas a la carpeta `src/`. La ejecución requiere que los archivos `MADRID UHI.zip` y `MADRID UP.zip` estén disponibles en `src/data/raw/`.

## 10. Limitaciones

- La muestra incluye 20 viviendas, 10 por grupo.
- D11 no dispone de electricidad.
- La cobertura temporal y las interrupciones no son iguales para todas las series.
- No se dispone de temperatura exterior, ocupación ni características constructivas detalladas.
- No se conoce la zona horaria documentada de los registros.
- Se mantienen valores energéticos negativos cuyo significado no está aclarado.
- Las correlaciones y comparaciones son descriptivas; no demuestran causalidad ni permiten generalizar a todas las viviendas.

## 11. Estado del proyecto

El notebook incluye las fases de obtención y validación, integración, limpieza y análisis exploratorio, además de conclusiones generales. La documentación final y la presentación se preparan como entregables complementarios.

## 12. Referencia

MODIF-HABIT. Dataset de monitorización energética residencial. Zenodo.  
[https://doi.org/10.5281/zenodo.20367908](https://doi.org/10.5281/zenodo.20367908)
