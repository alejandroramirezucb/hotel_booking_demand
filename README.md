# Hotel Booking Demand

## Orden de ejecución

Los notebooks están numerados y **deben ejecutarse en orden la primera vez**, porque el 03 genera
las particiones que consumen el 04 y el 05.

| Notebook | Criterios de la rúbrica | Requiere |
|---|---|---|
| `01_formulacion_y_variables.ipynb` | 1.1, 1.2, 2.1 | Nada |
| `02_estadistica_descriptiva.ipynb` | 2.2 | Nada |
| `03_calidad_desbalance_y_escalado.ipynb` | 2.3, 2.4, 2.5 | Nada. **Genera `datos_preparados.joblib`** |
| `04_entrenamiento_y_evaluacion.ipynb` | 3.1, 3.2, 3.3 | Notebook 03 |
| `05_discusion_y_conclusiones.ipynb` | 4.1, 4.2, 5.1 | Notebooks 03 y 04 |

Los notebooks 01 y 02 son independientes: cargan los datos desde la URL y pueden correrse en
cualquier momento.

## Cómo usarlos en Google Colab

1. Entrar a [colab.research.google.com](https://colab.research.google.com)
2. `Archivo → Subir cuaderno` y elegir el notebook
3. `Entorno de ejecución → Ejecutar todo`

La primera celda monta Google Drive y crea la carpeta `MyDrive/hotel_booking`, que es donde los
notebooks intercambian resultados y guardan los gráficos. Hay que autorizar el acceso la primera vez.

Si el montaje falla o no se autoriza, la celda **corta con un error explícito** en lugar de escribir
en el disco temporal de Colab, que se borra al cerrar la sesión.

Fuera de Colab los notebooks funcionan igual: si no detectan Colab, usan la carpeta local
`./hotel_booking` con la misma estructura.

## Datos

No hace falta descargar nada. Los notebooks leen el conjunto desde:

```
https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-02-11/hotels.csv
```

Son 16 MB, 119.390 reservas y 32 columnas. Fuente original: Antonio, N., Almeida, A. y Nunes, L.
(2019). *Hotel booking demand datasets*. Data in Brief, 22, 41–49.

## Tiempos aproximados

| Notebook | Duración |
|---|---|
| 01 | menos de 1 minuto |
| 02 | 1 a 2 minutos |
| 03 | 1 a 2 minutos |
| 04 | 3 a 6 minutos (entrena 13 modelos) |
| 05 | menos de 1 minuto |

## Archivos que se generan

En `MyDrive/hotel_booking/`:

```
hotel_booking/
├── datos_preparados.joblib        particiones train/test ya limpias (notebook 03)
├── modelo_y_resultados.joblib     modelo entrenado y predicciones (notebook 04)
├── barrido_hiperparametros.csv    resultados del barrido de C (notebook 04)
└── splits/                        los siete graficos en PNG a 200 dpi
```

## Gráficos

Cada notebook guarda sus figuras en `splits/` además de mostrarlas en pantalla. Los nombres llevan
como prefijo el notebook que los produce:

| Archivo | Notebook | Contenido |
|---|---|---|
| `02_boxplots_por_clase.png` | 02 | lead_time, adr y pedidos especiales por clase |
| `02_leadtime_y_tipo_deposito.png` | 02 | Distribución de lead_time y composición por tipo de depósito |
| `03_distribucion_de_clases.png` | 03 | Desbalance de la variable objetivo |
| `04_matriz_confusion_train.png` | 04 | Matriz de confusión sobre entrenamiento |
| `04_matriz_confusion_test.png` | 04 | Matriz de confusión sobre prueba |
| `05_regularizacion_vs_desempeno.png` | 05 | Curvas de F1 macro frente a `C` |
| `05_matriz_confusion_normalizada.png` | 05 | Matriz de confusión en porcentajes por fila |

La última celda del notebook 05 verifica que estén los siete.

