# Proyecto: Análisis exploratorio de datos para decisiones comerciales

## Introducción

Este repositorio aloja el proyecto del **Módulo 4: Análisis exploratorio de datos para decisiones comerciales**, perteneciente al **"Bootcamp Fundamentos de Ciencias de Datos 2026"** de **Talento Digital para Chile - SENCE**.

La empresa ficticia **ComercioYA** ha recolectado datos históricos del comportamiento de sus clientes (compras, visitas, montos, devoluciones y reseñas). Este proyecto aplica técnicas de Análisis Exploratorio de Datos (EDA) sobre ese dataset con el fin de detectar patrones, relaciones y valores atípicos que permitan sustentar decisiones estratégicas de ventas y marketing.

---

## Estructura del Proyecto

| Archivo / Carpeta | Descripción |
|---|---|
| [`main.ipynb`](./main.ipynb) | Cuaderno Jupyter que contiene todo el desarrollo EDA ([▶ Ver en nbviewer](https://nbviewer.org/github/c-mena/dsb26-eda/blob/main/)). |
| [`TECHNICAL_REPORT.md`](./TECHNICAL_REPORT.md) | Informe técnico con hallazgos, análisis, justificaciones y recomendaciones. |
| [`data/data_comercioya.csv`](./data/data_comercioya.csv) | Dataset sintético generado en la Lección 1 (exportado por `main.py`). |
| [`figures/`](./figures/) | Directorio que contiene todas las visualizaciones y gráficos estadísticos exportados en formatos PNG y PDF. |

---

## Requisitos y Tecnologías

| Librería | Uso |
|---|---|
| `numpy` | Generación de datos aleatorios y operaciones numéricas. |
| `pandas` | Manipulación y análisis del DataFrame. |
| `matplotlib` | Visualizaciones personalizadas y exportación de figuras. |
| `seaborn` | Gráficos estadísticos avanzados (pairplot, violin, heatmap, etc.). |
| `statsmodels` | Modelos de regresión lineal (OLS) con estadísticas de inferencia. |
| `scikit-learn` | Cálculo de métricas de error (MSE, MAE). |
| `ipykernel` | Ejecución del cuaderno en entorno Jupyter / VS Code. |

---

## Instalación y Despliegue Local

### 1. Clonar el repositorio

```bash
git clone https://github.com/c-mena/dsb26-eda
cd dsb26-eda
```

### 2. Crear e inicializar el entorno virtual con `uv`

Para asegurar la máxima reproducibilidad y eficiencia en la gestión de entornos, se recomienda usar [uv](https://docs.astral.sh/uv/). Esto ayuda aislar y no contaminar tu versión global de Python de forma extremadamente veloz.

```bash
uv venv
```

### 3. Activar el entorno virtual

```bash
# Windows
.venv\Scripts\activate

# macOS / Linux
source .venv/bin/activate
```

### 4. Instalar dependencias

Recomendamos instalar y sincronizar las bibliotecas requeridas utilizando el archivo `pyproject.toml` incluido en el proyecto, garantizando operar con las dependencias exactas y probadas:

```bash
uv sync
```

### 5. Ejecutar el proyecto

La alternativa recomendada para inicializar y observar el proyecto es emplear **Visual Studio Code (VS Code)** con su extensión de **Jupyter** instalada. Sólo debes abrir la carpeta del repositorio en VS Code, seleccionar tu entorno virtual `.venv` como tu Kernel de ejecución, y abrir el archivo `main.ipynb` para ejecutar el código y visualizar sus correspondientes anotaciones en simultáneo.

*(Otra alternativa válida, desde la consola y con tu entorno activo, es ejecutar el comando `jupyter notebook` para levantar el servidor y entrar a `main.ipynb` directamente mediante tu navegador web).*

---
