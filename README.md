# 🌧️ Antioquia Flood MLP — Predicción de Inundaciones con Red Neuronal Superficial

> **Fase 1 · Línea base** — Perceptrón Multicapa (MLP) para predicción de inundaciones en municipios de Antioquia, Colombia.

---

## ❓ Pregunta de investigación

> **¿Dado lo que ha llovido en las últimas horas en este municipio, va a inundarse en las próximas 24 horas?**

---

## 🧠 Arquitectura del modelo

| Componente | Detalle |
|---|---|
| **Tipo** | Shallow Neural Network — Perceptrón Multicapa (MLP) |
| **Capas ocultas** | 2 a 3 capas ocultas |
| **Función de activación** | ReLU |
| **Tipo de problema** | Clasificación binaria: inundación `1` / no inundación `0` |
| **Salida** | Sigmoid (probabilidad de inundación en las próximas 24 h) |

---

## 📥 Variables de entrada (features)

| # | Variable | Fuente | Descripción |
|---|---|---|---|
| 1 | Precipitación acumulada 6 h | IDEAM | Lluvia acumulada en las últimas 6 horas |
| 2 | Precipitación acumulada 12 h | IDEAM | Lluvia acumulada en las últimas 12 horas |
| 3 | Precipitación acumulada 24 h | IDEAM | Lluvia acumulada en las últimas 24 horas |
| 4 | Precipitación acumulada 48 h | IDEAM | Lluvia acumulada en las últimas 48 horas |
| 5 | Temperatura promedio | Open-Meteo | Temperatura media del municipio |
| 6 | Humedad relativa | Open-Meteo | Humedad relativa del municipio |
| 7 | Elevación media | DEM SRTM | Elevación media del municipio derivada del modelo digital de elevación |
| 8 | Cobertura impermeable | MapBiomas | Porcentaje de suelo impermeable del municipio |
| 9 | Distancia al río más cercano | Red hidrográfica IGAC | Distancia al cauce más cercano derivada de la red hidrográfica oficial |

---

## 🎯 Variable objetivo (Y)

| Valor | Significado |
|---|---|
| `1` | DAGRAN reportó inundación en el municipio en las **24 h siguientes** al evento |
| `0` | DAGRAN **no** reportó inundación en ese período |

---

## 🗂️ Fuentes de datos

| Fuente | Tipo de datos |
|---|---|
| [IDEAM](http://www.ideam.gov.co/) | Series de precipitación horaria por estación |
| [Open-Meteo](https://open-meteo.com/) | Temperatura y humedad relativa (API gratuita) |
| [NASA SRTM DEM](https://www2.jpl.nasa.gov/srtm/) | Modelo digital de elevación (resolución 30 m) |
| [MapBiomas Colombia](https://colombia.mapbiomas.org/) | Cobertura y uso del suelo (impervious surface) |
| [IGAC](https://www.igac.gov.co/) | Red hidrográfica oficial de Colombia |
| [DAGRAN](https://dagran.antioquia.gov.co/) | Reportes históricos de inundaciones en Antioquia |

---

## ✅ Justificación del modelo

El MLP es el **modelo base exigido como línea base interpretable**. Su simplicidad permite:

- Identificar qué variables tienen **mayor peso predictivo** antes de pasar a arquitecturas más complejas.
- Establecer métricas de referencia (F1, AUC-ROC, Recall) para comparar con modelos futuros.
- Interpretar los pesos de la red para validar el sentido físico de las variables climáticas e hidrológicas.

---

## 🗺️ Cobertura geográfica

- **Departamento:** Antioquia, Colombia
- **Unidad de análisis:** Municipio
- **Número de municipios:** 125

---

## 🔁 Flujo de trabajo

```
Datos crudos (IDEAM, Open-Meteo, SRTM, MapBiomas, IGAC)
        │
        ▼
Preprocesamiento & feature engineering
(ventanas temporales de precipitación, join por municipio)
        │
        ▼
Entrenamiento MLP (PyTorch / Keras)
        │
        ▼
Evaluación: F1 · AUC-ROC · Recall · Matriz de confusión
        │
        ▼
Interpretación de pesos & feature importance
```

---

## 🛠️ Stack tecnológico

- **Lenguaje:** Python 3.10+
- **Entorno de desarrollo:** Google Colab / Kaggle Notebooks
- **Frameworks de ML:** PyTorch o Keras (TensorFlow)
- **Manipulación de datos:** pandas, numpy
- **Datos geoespaciales:** geopandas, rasterio
- **Visualización:** matplotlib, seaborn

---

## 📁 Estructura del proyecto

```
antioquia-flood-mlp/
├── data/
│   ├── raw/            # Datos originales sin procesar
│   └── processed/      # Datos limpios y features generadas
├── notebooks/          # Jupyter / Colab notebooks
├── src/
│   ├── data/           # Scripts de descarga y preprocesamiento
│   ├── features/       # Ingeniería de características
│   └── models/         # Definición y entrenamiento del MLP
├── models/             # Modelos entrenados (.pt / .h5)
├── reports/            # Métricas, gráficas y resultados
├── requirements.txt
└── README.md
```

---

## 📊 Métricas de evaluación

Dado el desbalance esperado de clases (inundaciones son eventos poco frecuentes), se priorizan:

- **AUC-ROC** — capacidad discriminativa general
- **F1-score** — balance entre precisión y recall
- **Recall (sensibilidad)** — minimizar falsos negativos (inundaciones no detectadas)
- **Matriz de confusión** — análisis detallado de errores

---

## 👥 Equipo

Proyecto académico — Universidad de Antioquia  
Grupo: **Antioquia Flood AI**

---

## 📄 Licencia

Este proyecto está bajo la licencia incluida en el archivo [LICENSE](LICENSE).

