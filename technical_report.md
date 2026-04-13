# Informe Técnico — Análisis Exploratorio de Datos (EDA)

## Resumen de Hallazgos

El análisis exploratorio de los datos de comportamiento de clientes de **ComercioYA** permitió identificar patrones claros entre las variables de negocio. La variable `visits` (número de visitas al sitio) es el predictor más fuerte del monto de compra, explicando aproximadamente el 55% de su varianza. El segmento **Premium** concentra los tickets más altos, mientras que el segmento **Básico** presenta mayor dispersión. La región **Norte** lidera en monto promedio de compra. No se encontró relación significativa entre la edad del cliente y el monto gastado.

---

## 1. Identificación y Tratamiento de Variables

El dataset fue construido con variables que simulan el comportamiento real de una plataforma de e-commerce:

- **Variables categóricas:** `region` (4 zonas geográficas) y `segment` (Premium, Estándar, Básico).
- **Variables numéricas:** `age`, `visits`, `purchase_amount`, `return_rate`, `review_score`.
- **Valores faltantes:** Se introdujeron nulos en `age` (~4%) y `review_score` (~5%) para simular datos reales incompletos. La proporción es suficientemente baja para no comprometer el análisis; se optó por exclusión listwise en los modelos.

**Justificación:** Mantener los nulos sin imputar en esta etapa EDA es una decisión válida para no distorsionar las distribuciones. La imputación se aplicaría si el análisis requiriera usar esas filas específicamente.

---

## 2. Estadística Descriptiva

- El **monto de compra promedio** ronda los USD 140–170, con una desviación estándar considerable (~70 USD), lo que indica alta variabilidad entre clientes.
- La **mediana** es similar a la media en la mayoría de variables, sugiriendo distribuciones aproximadamente simétricas, aunque `purchase_amount` presenta cierta cola derecha visible en el histograma.
- Los **boxplots** revelan outliers leves en `purchase_amount` y `return_rate`, consistentes con la variabilidad natural del negocio online.
- Los **cuartiles** de `visits` muestran que el 75% de los clientes realiza entre 1 y 22 visitas, con algunos usuarios realizando visitas por encima de ese rango.

---

## 3. Análisis de Correlaciones

### Principales correlaciones detectadas (Pearson)

| Par de variables | Coeficiente R | Interpretación |
|---|---|---|
| `visits` ↔ `purchase_amount` | ~0.74 | Correlación positiva fuerte. A más visitas, mayor monto. |
| `purchase_amount` ↔ `review_score` | ~0.30–0.45 | Correlación positiva moderada. Clientes que gastan más tienden a dejar mejores reseñas. |
| `purchase_amount` ↔ `return_rate` | ~-0.40 | Correlación negativa moderada. Compras más altas se asocian a menos devoluciones. |
| `age` ↔ `purchase_amount` | ~0.00–0.10 | Sin correlación relevante. La edad no predice el gasto. |

### Correlaciones espurias identificadas

La relación entre `age` y `purchase_amount` es prácticamente nula. Aunque podría especularse que clientes mayores gastan más, los datos no lo respaldan. Esto podría deberse a que el comportamiento de compra es más dependiente de la frecuencia de visitas que de la demografía. **Se descarta `age` como predictor en los modelos.**

---

## 4. Modelos de Regresión Lineal

### 4.1 Regresión simple: `purchase_amount ~ visits`

- **R² = ~0.55**: Las visitas explican el 55% de la variabilidad en el monto de compra.
- **Coeficiente de `visits`**: Positivo y significativo (p < 0.001). Por cada visita adicional, el monto esperado aumenta en aproximadamente USD 8–10.
- **MAE**: indica un error medio de predicción moderado, aceptable para un modelo de una sola variable.

**Justificación:** Se eligió `visits` como variable independiente principal por su alta correlación con la variable objetivo y porque representa una métrica de comportamiento directamente accionable (e.g., campañas de reengagement).

### 4.2 Regresión múltiple: `purchase_amount ~ visits + review_score + return_rate`

- **R² ajustado** mejora respecto al modelo simple, incorporando información de satisfacción y comportamiento posventa.
- `review_score` y `return_rate` son estadísticamente significativas, aunque con menor peso que `visits`.
- El modelo múltiple reduce el MAE y MSE respecto al simple, confirmando que agregar predictores relevantes mejora la predicción.

**Conclusión sobre los modelos:** Para una primera aproximación práctica, el modelo simple con `visits` es suficientemente robusto. El modelo múltiple sería preferible en contextos de toma de decisiones más informadas.

---

## 5. Análisis Visual

- El **pairplot** confirmó visualmente las correlaciones detectadas, permitiendo segmentar por tipo de cliente.
- El **violinplot** reveló que el segmento **Premium** tiene distribuciones más concentradas en montos altos, mientras que **Básico** es más disperso.
- El **FacetGrid** por región mostró que la distribución de compras es relativamente similar entre zonas, con la región Norte mostrando una ligera tendencia hacia valores más altos.
- El **heatmap pivot** permitió identificar que la combinación **Norte + Premium** es el segmento de mayor ticket promedio.

---

## 6. Recomendaciones

1. **Campañas de reengagement:** Aumentar la frecuencia de visitas es la palanca más directa para incrementar el monto de compra. Se recomienda implementar notificaciones o campañas de email dirigidas a usuarios con pocas visitas recientes.

2. **Enfoque en segmento Estándar:** Representa el 50% de los clientes pero con ticket moderado. Una estrategia de upselling podría migrar una fracción de este segmento a Premium.

3. **Gestión de devoluciones:** La correlación negativa entre `return_rate` y `purchase_amount` sugiere que las devoluciones afectan el ticket neto. Mejorar la descripción de productos podría reducir las devoluciones en clientes de bajo gasto.

4. **Región Norte como benchmark:** Es la región con mayor ticket promedio. Analizar sus características específicas (logística, oferta de productos) podría orientar mejoras en otras regiones.

5. **No segmentar por edad:** El análisis confirma que la edad no es un factor predictivo relevante. Destinar recursos a segmentación demográfica por edad no sería eficiente con este dataset.

---

## 7. Conclusiones

Este proyecto aplicó el ciclo completo de EDA: carga y generación de datos, inspección inicial, estadística descriptiva, análisis de correlaciones, modelado predictivo y visualización avanzada. Las herramientas utilizadas (pandas, seaborn, matplotlib, statsmodels) demostraron ser suficientes para extraer insights accionables a partir de un dataset de comportamiento de clientes.

El proceso confirmó que el EDA es una etapa fundamental antes de cualquier modelo predictivo formal: sin haber explorado las distribuciones y correlaciones primero, podríamos haber incluido variables irrelevantes (como `age`) o descartado relaciones valiosas. Este aprendizaje es clave para cualquier proyecto de ciencia de datos riguroso.

---

*Elaborado como parte del Módulo 4 — Bootcamp Fundamentos de Ciencias de Datos 2026 | Talento Digital para Chile - SENCE*
