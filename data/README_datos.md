# Datos del proyecto — Swarovski Ecuador (2023–2025)

## Disponibilidad del dataset

El archivo `Swarovski_Dataset_Limpio_Anonimizado.csv` **no se incluye en este repositorio público** por acuerdo de confidencialidad con la organización. Los datos corresponden al sistema de facturación interno de Swarovski Ecuador y contienen información comercial sensible.

Para acceder al dataset, contactar a los autores del proyecto:

- Jhon Sánchez — Universidad de Las Américas
- Vinicio Betancourt — Universidad de Las Américas

---

## Descripción del dataset

| Característica | Valor |
|----------------|-------|
| Nombre del archivo | `Swarovski_Dataset_Limpio_Anonimizado.csv` |
| Formato | CSV codificación UTF-8 |
| Registros totales | 35,822 transacciones |
| Registros útiles (VENTA > 0) | 34,826 (97.2%) |
| Clientes únicos | 17,781 |
| Período cubierto | 1 enero 2023 → 31 diciembre 2025 |
| Número de columnas | 18 |
| Tamaño aproximado | ~5 MB |

---

## Estructura de columnas

| Columna | Tipo | Descripción | Ejemplo |
|---------|------|-------------|---------|
| `ANUAL` | int | Año de la transacción | 2023 |
| `MES` | str | Mes en español | Enero |
| `NUMERO` | int | Número de factura | 13135 |
| `VENDEDOR` | str | Código del vendedor | R.LORENA |
| `DESCRIPCION` | str | Descripción del producto | SWA SYMBOL:NECKLACE... |
| `CODIGO` | int | Código SKU del producto | 5497664 |
| `LINEA` | str | Línea de producto | JEWERLY |
| `SECCION` | str | Categoría de producto | COLLAR |
| `RUC_CLIENTE` | str | RUC/cédula anonimizado (SHA-256) | e48245556478c26c... |
| `NOMBRE_CLIENTE` | str | Nombre del cliente anonimizado (SHA-256) | 0b3578fd516ca716... |
| `BODEGA` | int | Código de tienda | 17 |
| `ZONA` | str | Nombre de la tienda | RIOCENTRO |
| `DOMICILIO` | str | Dirección del cliente | LOJA |
| `TELEFONO` | str | Teléfono anonimizado (SHA-256) | 27a696b038602edf... |
| `MAIL` | str | Email anonimizado (SHA-256) | 7119d1061ee76e1b... |
| `FECHADOCUMENTO` | str | Fecha de la transacción (ISO 8601) | 2023-01-01 |
| `UNIDADES` | int | Cantidad de unidades (negativo = devolución) | 1 |
| `VENTA` | float | Monto de venta en USD (negativo = devolución) | 191.35 |

---

## Notas de calidad del dataset

- **Nulos reales:** solo 3 registros (TELEFONO=1, MAIL=2) — no afectan el análisis
- **Duplicados:** 0 registros duplicados
- **Devoluciones:** 990 registros con VENTA < 0 y UNIDADES < 0 — excluidos del análisis
- **Transacciones vacías:** 3 registros con VENTA = 0 — excluidos del análisis
- **Formato de fecha:** ISO 8601 estricto (YYYY-MM-DD) — parsear con `format='%Y-%m-%d'`

> **Nota crítica de preprocesamiento:** el parámetro `dayfirst=True` de pandas genera 22,763 NaT artificiales con este dataset. Usar siempre `format='%Y-%m-%d'`.

---

## Secciones de producto disponibles

| Sección | Registros | % del total |
|---------|-----------|-------------|
| COLLAR | 10,747 | 30.0% |
| ARETES | 10,697 | 29.9% |
| PULSERA | 5,860 | 16.4% |
| ANILLO | 5,134 | 14.3% |
| BOLIGRAFOS | 2,017 | 5.6% |
| INDETERMINADO | 812 | 2.3% |
| RELOJ Y SUS ACCESORIOS | 394 | 1.1% |
| FAMILIA 70-80 | 98 | 0.3% |
| HOME | 37 | 0.1% |
| LLAVEROS, MOBILE PHONE Y CHARM | 17 | 0.0% |
| PRENDEDORES Y GEMELOS | 9 | 0.0% |

---

## Tiendas (zonas) disponibles

| Zona | Registros | % del total |
|------|-----------|-------------|
| QUICENTRO | 11,612 | 32.4% |
| SCALA | 6,935 | 19.4% |
| RIOCENTRO | 6,151 | 17.2% |
| JARDIN | 4,195 | 11.7% |
| SAN MARINO | 3,832 | 10.7% |
| NORTE | 2,364 | 6.6% |
| CUMBAYA | 345 | 1.0% |
| CENTRO | 182 | 0.5% |
| SAMBORONDON | 92 | 0.3% |
| SUR | 64 | 0.2% |
| URDESA | 46 | 0.1% |
| NO REGISTRADO | 3 | 0.0% |
| ECOMMERCE | 1 | 0.0% |

---

## Consideraciones éticas y legales

- Los datos fueron anonimizados mediante **SHA-256** sobre las columnas RUC_CLIENTE, NOMBRE_CLIENTE, TELEFONO y MAIL antes de ser utilizados en este proyecto
- La anonimización es **irreversible** — no es posible re-identificar clientes a partir del dataset
- El procesamiento cumple con la **Ley Orgánica de Protección de Datos Personales del Ecuador (2021)**
- El dataset es de uso exclusivo para fines académicos del presente proyecto de titulación

---

## Cómo colocar el dataset para ejecutar el pipeline

1. Descargar o solicitar el archivo `Swarovski_Dataset_Limpio_Anonimizado.csv`
2. Subirlo a Google Drive en la ruta:
   ```
   /MyDrive/Proyecto_Swarovski/Swarovski_Dataset_Limpio_Anonimizado.csv
   ```
3. Verificar que la constante `FILE_DATASET` en el BLOQUE 1 del notebook coincida con el nombre del archivo:
   ```python
   FILE_DATASET = 'Swarovski_Dataset_Limpio_Anonimizado.csv'
   ```
