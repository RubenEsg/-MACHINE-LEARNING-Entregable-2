# Entrega 2 — Preparación de datos y modelos base

**Universidad del Norte — Machine Learning**

Martínez Pulido, Valerie · Basto Martínez, Abrahan · Esguerra Fernández, Rubén

Auditoría de calidad de datos y modelos lineales de referencia para la predicción de fuga de
clientes en una fintech colombiana. Continúa el
[análisis exploratorio](https://rubenesg.github.io/Machine_learning/) de la Entrega 1.

## Contenido

| Archivo | Descripción |
|---|---|
| `entrega2_modelo.ipynb` | Cuaderno completo, **ejecutado de principio a fin**: procesamiento, auditoría de la etiqueta, clasificación logística con Ridge/Lasso, regresión Ridge/Lasso sobre el objetivo continuo y referencia KNN |
| `Entrega2.pdf` | Artículo con la metodología y los resultados |
| `manuscrito_fuente/` | Fuente editable del artículo (HTML y figuras) |

## Datos

El conjunto **no está en este repositorio** porque es público y pesa 136 MB
(`transactions_data.csv` supera el límite de 100 MB por archivo de GitHub).

Se trata de COFINFAD — *Colombian Fintech Financial Analytics Dataset*, disponible en
[Mendeley Data](https://data.mendeley.com/datasets/mhb4zn3258/1)
(DOI: 10.17632/mhb4zn3258.1), bajo licencia CC BY 4.0.

Para reproducir el cuaderno, descargue `customer_data.csv` y `transactions_data.csv` y
ubíquelos en una carpeta `datos/` junto al cuaderno:

```
.
├── entrega2_modelo.ipynb
└── datos/
    ├── customer_data.csv
    └── transactions_data.csv
```

La ruta se resuelve de forma relativa, de modo que no hace falta editar nada.

## Entorno

Python 3.13.3 · numpy 2.2.6 · pandas 2.3.3 · scikit-learn 1.7.2 · semilla 42.
El cuaderno tarda unos 150 s en ejecutarse por completo.

```bash
pip install numpy pandas matplotlib seaborn scikit-learn jupyter
```

## Resultados principales

- La etiqueta `churn_probability` está construida a partir de `active_products`: incluir esa
  columna lleva el R² de 0,151 a 0,921 y el AUC de 0,682 a 0,974. Se excluye del modelo.
- Clasificación: regresión logística con penalización L1 (`C` = 0,1), **AUC de 0,6832 en prueba**,
  exhaustividad 0,6515, 57 de 78 variables.
- Regresión: Lasso (`alpha` = 0,0001), **R² = 0,1511**, RMSE 0,0617.
- El comportamiento transaccional no aporta capacidad predictiva (AUC de 0,5016 en solitario).
- Un KNN (k = 200) alcanza 0,6645, por debajo del modelo lineal.
