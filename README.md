# Submuestreo y análisis de datos gravimétricos y magnetométricos

Este repositorio contiene datasets de gravimetría y magnetometría generados a partir de modelos sintéticos, junto con diferentes estrategias de submuestreo, métricas espaciales y visualizaciones asociadas.

---
## Generación de datos

Los datasets fueron generados a partir de un flujo de trabajo sintético:

1. Construcción de modelos geológicos mediante **GemPy**
2. Simulación de adquisición geofísica (gravimetría y magnetometría) mediante **SimPEG**
3. Aplicación de estrategias de submuestreo

---

## Estructura del repositorio

Cada carpeta corresponde a un número fijo de puntos (`n_total`):

```text
submuestreo/
│
├── n_44/
├── n_88/
├── n_120/
│   ├── dataset_aleatorio_nXX.txt
│   ├── dataset_sistematico_nXX.txt
│   ├── dataset_clustering_nXX.txt
│   ├── dataset_cuadrantes_nXX.txt
│   ├── metricas_nXX.csv
│   ├── cv_vs_dmean_nXX.png
│   ├── ssim_multiquadric_nXX.png
│
└── dataset_original.txt
```

---

## Descripción de los datos

Cada dataset contiene cuatro columnas:

```text
X   Y   Z   Valor
```

* X, Y: coordenadas espaciales
* Z: elevación
* Valor: anomalía gravimétrica (mGal) o respuesta magnética (nT)

---

## Métodos de submuestreo

Se aplicaron diferentes estrategias para simular condiciones de adquisición:

* Aleatorio: selección uniforme sin patrón espacial
* Sistemático: selección regular basada en índice
* Clustering: selección basada en agrupamiento (KMeans)
* Cuadrantes: distribución ponderada por regiones espaciales

---

## Métricas espaciales

Para cada dataset se calcularon métricas basadas en la distancia al vecino más cercano:

* d_mean: espaciamiento promedio
* d_std: desviación estándar del espaciamiento
* d_min / d_max: valores extremos
* CV (coeficiente de variación):

CV = σ / μ

σ = desviación estándar del espaciamiento entre puntos

μ = espaciamiento promedio

Interpretación del CV:

| Rango     | Interpretación |
| --------- | -------------- |
| < 0.1     | Muy uniforme   |
| 0.1 – 0.3 | Regular        |
| 0.3 – 0.6 | Irregular      |
| > 0.6     | Muy irregular  |

---

## Visualizaciones

### CV vs espaciamiento promedio

Permite analizar el balance entre:

* Resolución espacial (d_mean)
* Regularidad del muestreo (CV)

Se incluye una línea de referencia en 500 m, representando un espaciamiento típico de estudios semi-detallados.

---

### Interpolación y comparación (SSIM)

Se generaron grillas interpoladas mediante RBF multiquadric.

La similitud estructural (SSIM) se calcula respecto al dataset original (ground truth), permitiendo evaluar la pérdida de información causada por el submuestreo.

---

## Consideraciones

* Un bajo CV no garantiza una adecuada cobertura espacial global
* Un espaciamiento reducido no implica necesariamente mejor calidad de interpolación
* La geometría del muestreo tiene un impacto significativo en los resultados

---

## Uso

Los datasets pueden utilizarse para:

* Evaluación de métodos de interpolación
* Entrenamiento y validación de modelos de aprendizaje automático
* Análisis de sensibilidad a la densidad y geometría de muestreo

---

## Notas

Este conjunto de datos fue generado con fines de investigación en geofísica aplicada, particularmente en el análisis de estrategias de interpolación bajo condiciones de muestreo irregular y escaso, utilizando modelos sintéticos controlados.

---

## Autor

Andres Felipe Guevara

Maestría en Geofísica - Universidad Industrial de Santander
