# Segmentación Inteligente de Clientes — Joyería de Lujo (2023–2025)

**Proyecto de Titulación — Maestría en Inteligencia Artificial Aplicada**
**Universidad de Las Américas (UDLA)**
**Autores:** Jhon Sánchez · Vinicio Betancourt
**Versión del pipeline:** v5.0
**Última actualización:** Abril 2026

---

## Descripción del problema y solución

Una cadena de joyería de lujo con cinco tiendas físicas acumula más de 34,000
transacciones históricas (2023–2025) que permanecen subutilizadas para la toma
de decisiones comerciales. El análisis exploratorio reveló que el **88% de los
clientes están inactivos** y el **85% son clientes que realizaron una única
compra** sin retorno posterior.

Este proyecto desarrolla un **pipeline de inteligencia artificial** que
transforma datos transaccionales históricos en perfiles de cliente accionables,
analizados en cuatro dimensiones complementarias:

| Dimensión | Algoritmo final | K | Silhouette |
|-----------|----------------|---|-----------|
| RFM (Recencia, Frecuencia, Monetario) | Jerárquico Average | 4 | 0.6246 |
| Afinidad de Producto | K-Means | 5 | 0.5814 |
| Ciclo de Vida del Cliente | K-Means | 3 | 0.8995 |
| Valor / Margen Financiero | K-Means | 4 | 0.4663 |

El pipeline culmina en un **motor de recomendación estratégica** que asigna
una de cinco acciones diferenciadas a cada cliente (VIP, Win-Back, Cross-Sell,
Retención, Nutrición), exportable en formato Excel para uso inmediato por el
equipo comercial.

---

## Estructura del repositorio

```
Proyecto_Swarovski/
│
├── data/
│   ├── README_datos.md
│   └── Dataset_Sintetico_Joyeria.csv
│
├── notebooks/
│   ├── Swarovski_Segmentacion_v5_SinteticoFase2.ipynb
│   ├── Swarovski_Segmentacion_v5_Fase2.ipynb
│   ├── Swarovski_Segmentacion_v5_Fase1.ipynb
│   ├── Generar_Dataset_Sintetico.ipynb
│   └── Anonimizar_dataset.ipynb
│
├── scripts/
│   ├── swarovski_segmentacion_v5_sinteticofase2.py
│   ├── swarovski_segmentacion_v5_fase2.py
│   ├── swarovski_segmentacion_v5_fase1.py
│   ├── generar_dataset_sintetico.py
│   └── anonimizar_dataset.py
│
├── resultados/
│   ├── SEGMENTACION_MULTIVARIABLE_SWAROVSKI_FINAL_Sintetico.xlsx
│   ├── Figura_4_Codo_Silhouette_RFM.png
│   ├── Figura_5_Segmentos_RFM.png
│   ├── Figura_6_Afinidad_Producto.png
│   ├── Figura_7_Ciclo_Vida.png
│   ├── Figura_8_Radar_Valor.png
│   ├── Figura_9_XAI_Variables.png
│   └── Figura_10_Sensibilidad_K.png
│
└── README.md
```

---

## Descripción de archivos por carpeta

### data/

| Archivo | Descripción |
|---------|-------------|
| `README_datos.md` | Documentación completa del dataset real (columnas, distribución, notas de calidad, consideraciones éticas). El dataset real no se incluye por acuerdo de confidencialidad con la organización. |
| `Dataset_Sintetico_Joyeria.csv` | Dataset completamente sintético con las mismas 18 columnas que el dataset real. Generado con distribuciones plausibles para el sector de joyería de lujo. Permite ejecutar y verificar el pipeline completo sin acceder a datos confidenciales. **No contiene datos reales de ningún cliente ni empresa.** |

### notebooks/

| Archivo | Descripción | Datos utilizados |
|---------|-------------|-----------------|
| `Swarovski_Segmentacion_v5_Fase1.ipynb` | Pipeline completo en FASE 1 — búsqueda automática del K óptimo estadístico en el rango [2,11] para cada dimensión. Incluye outputs ejecutados. | Dataset real |
| `Swarovski_Segmentacion_v5_Fase2.ipynb` | Pipeline completo en FASE 2 — K estratégico fijo de negocio (RFM=4, Producto=5, Ciclo=3, Valor=4). Incluye outputs ejecutados con resultados finales del proyecto. | Dataset real |
| `Swarovski_Segmentacion_v5_SinteticoFase2.ipynb` | Pipeline FASE 2 ejecutado sobre el dataset sintético. Permite reproducir y verificar el funcionamiento completo del pipeline sin requerir el dataset confidencial. | Dataset sintético |
| `Generar_Dataset_Sintetico.ipynb` | Notebook autocontenido que genera el archivo `Dataset_Sintetico_Joyeria.csv`. Ejecutar antes de usar el notebook sintético. | — |
| `Anonimizar_dataset.ipynb` | Evidencia del proceso de anonimización SHA-256 aplicado offline al dataset crudo. Se incluye como documentación del proceso; requiere el CSV crudo para ejecutarse. | Dataset crudo (no incluido) |

### scripts/

| Archivo | Descripción |
|---------|-------------|
| `swarovski_segmentacion_v5_fase1.py` | Código fuente del pipeline en configuración FASE 1 (K_FINAL = None en todas las dimensiones). |
| `swarovski_segmentacion_v5_fase2.py` | Código fuente del pipeline en configuración FASE 2 (K estratégicos fijos). Versión de producción. |
| `swarovski_segmentacion_v5_sinteticofase2.py` | Código fuente del pipeline configurado para ejecutarse con el dataset sintético (FILE_DATASET apunta a Dataset_Sintetico_Joyeria.csv). |
| `generar_dataset_sintetico.py` | Script Python standalone que genera el dataset sintético. Alternativa al notebook homónimo para ejecución local. |
| `anonimizar_dataset.py` | Script de anonimización SHA-256. Evidencia del proceso aplicado al dataset crudo. No ejecutable sin el CSV original. |

### resultados/

| Archivo | Descripción | Datos |
|---------|-------------|-------|
| `SEGMENTACION_MULTIVARIABLE_SWAROVSKI_FINAL_Sintetico.xlsx` | Dataset maestro con todos los clientes segmentados en las 4 dimensiones y su acción estratégica recomendada. Generado con el pipeline sintético (BLOQUE 10). | Sintéticos |
| `Figura_4_Codo_Silhouette_RFM.png` | Método del Codo y Silhouette Score — selección de K, dimensión RFM. | Reales (agregados) |
| `Figura_5_Segmentos_RFM.png` | Visualización de segmentos RFM — FASE 2 (K=4). | Reales (agregados) |
| `Figura_6_Afinidad_Producto.png` | Distribución de afinidad por categoría de producto — FASE 2 (K=5). | Reales (agregados) |
| `Figura_7_Ciclo_Vida.png` | Visualización 2D de segmentos Ciclo de Vida — FASE 2 (K=3). | Reales (agregados) |
| `Figura_8_Radar_Valor.png` | Radar comparativo de segmentos Valor/Margen — FASE 2 (K=4). | Reales (agregados) |
| `Figura_9_XAI_Variables.png` | Importancia de variables XAI por rango de centroides. | Reales (agregados) |
| `Figura_10_Sensibilidad_K.png` | Sensibilidad del modelo ante variación de K — dimensión RFM. | Reales (agregados) |

> Las figuras muestran métricas y visualizaciones agregadas del modelo. No contienen datos individuales de clientes y corresponden a los resultados publicados en el informe final de titulación.

---

## Nota sobre confidencialidad y reproducibilidad

El dataset real de la organización **no se incluye en este repositorio** por
acuerdo de confidencialidad. El repositorio está diseñado para garantizar
reproducibilidad completa mediante el dataset sintético:

**Flujo recomendado para evaluadores:**

```
1. Ejecutar Generar_Dataset_Sintetico.ipynb
        ↓ genera Dataset_Sintetico_Joyeria.csv
2. Subir CSV a Google Drive en /MyDrive/Proyecto_Swarovski/data/
        ↓
3. Ejecutar Swarovski_Segmentacion_v5_SinteticoFase2.ipynb
        ↓ produce segmentos + Excel + visualizaciones
4. Comparar resultados con los notebooks reales (Fase1 y Fase2)
        ↓ valida que el pipeline funciona correctamente
```

**Para los autores (con acceso al dataset real):**

```
1. Colocar dataset real en /MyDrive/Proyecto_Swarovski/data/
2. Ejecutar Swarovski_Segmentacion_v5_Fase1.ipynb  →  resultados FASE 1
3. Ejecutar Swarovski_Segmentacion_v5_Fase2.ipynb  →  resultados FASE 2
```

---

## Requisitos técnicos y dependencias

### Plataforma de ejecución
- **Google Colab** (recomendado) — entorno gratuito, no requiere instalación local
- **Python 3.10+**
- **Google Drive** — para montar el dataset

### Librerías principales

| Librería | Versión mínima | Uso |
|----------|---------------|-----|
| pandas | 1.5 | Procesamiento de datos |
| numpy | 1.23 | Cálculo numérico |
| scikit-learn | 1.2 | Algoritmos de clustering y métricas |
| matplotlib | 3.6 | Visualizaciones estáticas |
| seaborn | 0.12 | Visualizaciones EDA |
| plotly | 5.13 | Visualizaciones interactivas 3D |
| ipywidgets | 8.0 | Panel interactivo en BLOQUE 10 |
| openpyxl | 3.1 | Exportación a Excel |

### Instalación en Colab (si alguna librería no está disponible)

```python
!pip install scikit-learn matplotlib seaborn plotly ipywidgets openpyxl
```

---

## Instrucciones de ejecución paso a paso

### Paso 1 — Preparar Google Drive

Crear la siguiente estructura en Google Drive:

```
Mi unidad/
└── Proyecto_Swarovski/
    └── data/
        └── Dataset_Sintetico_Joyeria.csv
```

### Paso 2 — Abrir el notebook en Colab

1. Ir a [colab.research.google.com](https://colab.research.google.com)
2. **Archivo → Subir notebook**
3. Seleccionar `Swarovski_Segmentacion_v5_SinteticoFase2.ipynb`

### Paso 3 — Verificar configuración en BLOQUE 1

Confirmar que las constantes están configuradas correctamente:

```python
# Ruta del dataset
PATH_DRIVE   = '/content/drive/MyDrive/Proyecto_Swarovski/data'
FILE_DATASET = 'Dataset_Sintetico_Joyeria.csv'

# K estratégicos FASE 2
K_FINAL_RFM      = 4
K_FINAL_PRODUCTO = 5
K_FINAL_CICLO    = 3
K_FINAL_VALOR    = 4
```

### Paso 4 — Ejecutar el pipeline completo

```
Entorno de ejecución → Ejecutar todo   (Ctrl + F9)
```

> **Importante:** ejecutar siempre desde BLOQUE 0. Si el runtime se reinicia,
> volver a ejecutar desde el inicio.
> Tiempo estimado: **2–4 minutos** con el dataset sintético.

### Paso 5 — Exportar resultados

Al finalizar el BLOQUE 10, hacer clic en:

```
📥 Generar y Descargar Excel
```

---

## Explicación general del pipeline

El pipeline está organizado en **11 bloques de código Colab**:

| Bloque | Nombre | Función principal |
|--------|--------|-------------------|
| BLOQUE 0 | Gobernanza | Declaración de privacidad y anonimización |
| BLOQUE 1 | Imports y constantes | Hiperparámetros globales y configuración de FASE |
| BLOQUE 2 | Ingesta y EDA | Carga del dataset, corrección de fechas, 9 visualizaciones |
| BLOQUE 3 | Preprocesamiento | Limpieza y construcción de 4 datasets por cliente |
| BLOQUE 4 | Segmentación RFM | K=4, Jerárquico Average — 4 arquetipos de cliente |
| BLOQUE 5 | Segmentación Producto | K=5, K-Means — 5 categorías de afinidad |
| BLOQUE 6 | Segmentación Ciclo de Vida | K=3, K-Means — Leales, En Riesgo, Fugaces |
| BLOQUE 7 | Segmentación Valor/Margen | K=4, K-Means — Ballena, Alto, Medio, Bajo |
| BLOQUE 8 | Validación y robustez | 3 pruebas de sensibilidad |
| BLOQUE 9 | XAI y ética | Centroides, importancia de variables, análisis ético |
| BLOQUE 10 | Consolidación y exportación | Merge 4 dimensiones, motor de recomendación, Excel |

---

## Parámetros de producción (FASE 2)

| Parámetro | Valor | Descripción |
|-----------|-------|-------------|
| `RANDOM_STATE` | 42 | Semilla global para reproducibilidad |
| `N_INIT` | 10 | Inicializaciones de K-Means |
| `K_MIN / K_MAX` | 2 / 11 | Rango de búsqueda en FASE 1 |
| `PERC_LOW / PERC_HIGH` | 1 / 99 | Clipping de VENTA |
| `DBSCAN_MIN_S` | 5 | Mínimo de muestras para DBSCAN |
| `WINSOR_VALOR` | 95 | Percentil de winsorización en Valor/Margen |
| `K_FINAL_RFM` | 4 | K estratégico RFM |
| `K_FINAL_PRODUCTO` | 5 | K estratégico Producto |
| `K_FINAL_CICLO` | 3 | K estratégico Ciclo de Vida |
| `K_FINAL_VALOR` | 4 | K estratégico Valor/Margen |

---

## Control de versiones

| Versión | Cambio principal |
|---------|-----------------|
| v1.0 | Baseline: RFM + K-Means + log1p + StandardScaler — 1 dimensión |
| v3.0 | RobustScaler + DBSCAN + Jerárquico + 4 dimensiones |
| v4.0 | Normalización por fila en Producto + INDICE_ABANDONO + winsorización P95 |
| v5.0 | Fix bug fecha · K=5 Producto · benchmark_tres_algoritmos · motor de recomendación · panel interactivo · dataset sintético |

---

## Consideraciones éticas

- Los datos reales están **anonimizados con SHA-256** sobre RUC, nombre,
  teléfono y email — proceso documentado en `scripts/anonimizar_dataset.py`
- El dataset sintético fue construido con distribuciones plausibles pero
  **no refleja datos reales** de ningún cliente ni empresa
- El modelo usa **exclusivamente variables de comportamiento de compra**,
  sin perfiles demográficos ni socioeconómicos
- El motor de recomendación **sugiere acciones**, no las ejecuta —
  supervisión humana obligatoria
- Se recomienda **re-entrenamiento cada 6 meses** o cuando la distribución
  de ventas cambie más del 20%
- Cumple con la **Ley Orgánica de Protección de Datos Personales
  del Ecuador (2021)**

---

## Referencia al informe final

> Sánchez, J., y Betancourt, V. (2026). *Segmentación inteligente de clientes
> mediante algoritmos de clustering no supervisado: Caso aplicado en retail de
> joyería de lujo (2023–2025)*. Proyecto de titulación, Maestría en
> Inteligencia Artificial Aplicada, Universidad de Las Américas.
