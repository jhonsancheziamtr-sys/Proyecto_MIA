# Demo — Dashboard Interactivo de Segmentación

**Proyecto:** Segmentación Inteligente de Clientes · Swarovski Ecuador (2023–2025)  
**Pipeline:** v5.0 | **Autores:** Jhon Sánchez · Vinicio Betancourt  
**Programa:** Maestría en Inteligencia Artificial Aplicada — UDLA

---

## Contenido

| Archivo | Descripción |
|---|---|
| `Dashboard_Segmentacion_Swarovski.html` | Dashboard interactivo del BLOQUE 10 del pipeline |

---

## Cómo usar el dashboard

### Opción A — Datos demo (sin archivos adicionales)
1. Abre `Dashboard_Segmentacion_Swarovski.html` directamente en cualquier navegador
2. El dashboard carga automáticamente **500 clientes sintéticos** generados con semilla `2025` para demostración reproducible
3. No requiere instalación ni servidor

### Opción B — Datos reales del pipeline
1. Ejecuta el pipeline completo siguiendo las instrucciones del [Anexo 3](../README.md)
2. Al finalizar el BLOQUE 10, descarga el archivo `SEGMENTACION_MULTIVARIABLE_SWAROVSKI_FINAL.xlsx`
3. Abre el dashboard y usa el botón **"Subir Excel o CSV del BLOQUE 10"**
4. Selecciona el archivo `.xlsx` generado por el pipeline

---

## Columnas requeridas en el archivo de entrada

El dashboard espera las siguientes columnas (generadas automáticamente por el BLOQUE 10):

```
NOMBRE_CLIENTE · RECENCIA · FRECUENCIA · MONETARIO
PERFIL_CLIENTE · PERFIL_PRODUCTO · SEGMENTO_VIDA
SEGMENTO_VALOR · VENTA_TOTAL_REAL · ACCION_SUGERIDA
```

---

## Funcionalidades

- Resumen ejecutivo con KPIs de los 4 segmentos
- Filtros interactivos por dimensión (RFM, Producto, Ciclo de Vida, Valor)
- Tabla de clientes con búsqueda en tiempo real
- Visualización de distribución por acción estratégica recomendada
- Compatible con Chrome, Firefox, Edge y Safari

---

## Nota de privacidad

El archivo de resultados real (`SEGMENTACION_MULTIVARIABLE_SWAROVSKI_FINAL.xlsx`) **no se distribuye en este repositorio** por contener datos anonimizados de clientes del sponsor, protegidos bajo la Ley Orgánica de Protección de Datos Personales del Ecuador (Asamblea Nacional del Ecuador, 2021).

Los datos de demostración incluidos en el HTML son completamente sintéticos y no corresponden a clientes reales.

---

## Dependencias

Ninguna. El dashboard es un archivo HTML autocontenido que carga SheetJS y Chart.js desde CDN en el momento de abrir el archivo.

```
Chart.js  — visualizaciones
SheetJS   — lectura de archivos Excel/CSV
```
