# Datos

Todos los datos son del Instituto Nacional de Estadística y Censos de Costa Rica (INEC).

| Fuente | Archivo | Uso | En el repositorio |
|---|---|---|---|
| [Encuesta Nacional de Hogares](https://www.inec.cr/encuestas/encuesta-nacional-de-hogares), 2010-2025 | Un archivo `.sav` por año | Empleo, horas, ingresos, aseguramiento y composición del hogar | No |
| [Estadísticas Vitales de Nacimientos](https://www.inec.cr/estadisticas-vitales), 2005-2024 | `Nacimientos2005-2024.sav` | Edad de la madre y número de hijos en cada nacimiento, para validar la encuesta | No |
| Estadísticas demográficas, 1950-2024 | `raw/ESTADISTICAS_DEMOG1950_2024.xlsx` | Tasa global de fecundidad | Sí |

Los microdatos y las bases que se arman con ellos (`data/processed/*.parquet`) no se publican, porque los distribuye el INEC y no se pudieron confirmar sus condiciones de redistribución. Los cuadernos ya ejecutados muestran todos los resultados.

## Cómo reconstruir las bases

Los archivos del INEC van en `data/raw/inec/`, organizados como se muestra abajo. Cada archivo de la ENAHO puede conservar el nombre con que lo publica el INEC, siempre que contenga el año.

```text
data/raw/inec/Enaho/ENAHO 2010.sav
data/raw/inec/Enaho/ENAHO 2011.sav
...
data/raw/inec/Enaho/ENAHO 2025.sav
data/raw/inec/Nacimientos/Nacimientos2005-2024.sav
```

Luego se corre `notebooks/1_base_de_datos.ipynb`. Si los archivos están en otra carpeta, se indica en la variable de entorno `DATOS_INEC` o en la primera celda del cuaderno. El cuaderno genera `data/processed/personas.parquet`, con 330.255 personas de 15 a 55 años de 2010 a 2025 y los hijos que viven con ellas, y `data/processed/nacimientos.parquet`, con 1.034.443 nacimientos de 2009 a 2024. Las Estadísticas Vitales llegan a 2024, su último año publicado. El cuaderno explica cómo se construye cada variable.
