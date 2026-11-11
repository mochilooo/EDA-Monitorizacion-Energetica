# Registro detallado de cambios

## Revisión integral de noviembre de 2026

### Conservación y alcance

- Se preservó una copia binaria del paquete de entrada en `original/EDA-Monitorizacion-Energetica_original.zip`.
- Los ZIP de datos fuente permanecen sin modificaciones en `src/data/raw/`.
- La tabla integrada y el contenido analítico válido se conservaron. No se eliminaron viviendas, variables ni observaciones.

### Notebook

- Se documentó un criterio explícito de completitud diaria: al menos 72 de los 96 registros nominales de 15 minutos, equivalente al 75 % de cobertura.
- Se añadieron recuentos diarios por variable y una tabla que informa la proporción de días que supera el umbral.
- Las series descriptivas conservan los días disponibles. El filtro de cobertura se aplica únicamente a correlaciones y a los indicadores por vivienda.
- H01 y H02 exigen al menos 30 días emparejados y suficientemente cubiertos por vivienda.
- Se actualizó la interpretación para distinguir el control de cobertura de un control causal o de estacionalidad.
- Se limpiaron las salidas heredadas del notebook para evitar que resultados previos aparezcan como si correspondieran al código revisado.

### Resultados de sensibilidad de cobertura

| Asociación | Mediana anterior | Mediana con 75 % de cobertura | Viviendas |
|---|---:|---:|---:|
| Temperatura y electricidad | -0,141 | -0,197 | 19 |
| Temperatura y gas | -0,703 | -0,668 | 20 |
| Humedad y electricidad | +0,165 | +0,179 | 19 |
| Humedad y gas | +0,396 | +0,403 | 20 |

La dirección de las asociaciones y la conclusión exploratoria principal se mantienen. Estas cifras no demuestran causalidad y no sustituyen un análisis que controle estacionalidad, ocupación o condiciones exteriores.

### Memoria y presentación

- Se generó una memoria revisada con un anexo metodológico, la regla de cobertura y la tabla de sensibilidad.
- Se actualizó la presentación con el criterio de cobertura y las cuatro medianas recalculadas.
- Se mantuvieron las versiones originales de ambos entregables junto a sus versiones mejoradas.

### Cambios que no se realizaron

- No se imputaron ausencias.
- No se sustituyeron valores negativos por cero.
- No se eliminaron atípicos, viviendas ni periodos.
- No se presentaron asociaciones como relaciones causales.
