# Proyecto Bootcamp TripleTen -  Análisis de Movilidad Urbana y Productividad Económica

## 📋 Descripción del Proyecto

Este proyecto analiza la relación entre la **movilidad urbana** (congestión vehicular, tiempos de viaje) y la **productividad económica** (PIB per cápita, desempleo) en las principales ciudades del mundo. Los resultados obtenidos servirán como base para que instituciones financieras como el Banco Interamericano de Desarrollo (BID) identifiquen ciudades prioritarias para inversión en infraestructura de transporte.

El análisis integra dos fuentes de datos reales:
- **TomTom Traffic Index**: Datos de tráfico en tiempo real
- **OECD Cities**: Indicadores económicos y sociales urbanos

---

## 🎯 Objetivo General

Crear un dataset limpio y unificado que permita:
- Identificar ciudades con alta congestión y baja productividad económica
- Reconocer ciudades con indicadores óptimos combinados
- Analizar correlaciones entre movilidad urbana y desarrollo económico
- Generar insights para decisiones de inversión en infraestructura de transporte

---

## 📊 Preguntas de Negocio

- ¿Qué ciudades presentan alta congestión y baja productividad económica?
- ¿Cuáles ciudades muestran los mejores indicadores combinados?
- ¿Qué variables tienen una relación más fuerte con el desarrollo urbano?
- ¿En qué ciudades debería enfocarse la inversión en infraestructura de transporte?

---

## 📁 Estructura del Proyecto

```
.
├── README.md                              # Este archivo
├── S5_ladb_mobility_economy_analysis.ipynb # Notebook principal del análisis
├── data/
│   ├── raw/
│   │   ├── tomtom_traffic.csv            # Datos de tráfico (TomTom)
│   │   └── oecd_city_economy.csv         # Datos económicos (OECD)
│   └── processed/
│       └── mobility_economy_unified.csv  # Dataset final limpio y unificado
└── output/
    └── analysis_results.ladb_mobility_economy_2024_clean             # Visualizaciones y reportes
```

---

## 📊 Fuentes de Datos

### Dataset 1: `tomtom_traffic.csv`
**Fuente**: TomTom Traffic Index

Contiene información sobre niveles de tráfico y congestión en tiempo real de ciudades monitoreadas globalmente.

**Características principales:**
- `Country`: País de la ciudad
- `City`: Nombre de la ciudad
- `UpdateTimeUTC`:  Marca de tiempo que indica la hora exacta de la última actualización, expresada en formato UTC 
- `Congestion Level`: Nivel de congestión (%)
- `Average Speed`: Velocidad promedio de circulación (km/h)
- Variables de comparación (vs. semana anterior)

**Cardinalidad**: Múltiples registros por ciudad (datos históricos/actualizaciones)

---

### Dataset 2: `oecd_city_economy.csv`
**Fuente**: OECD Cities

Contiene indicadores económicos, laborales y ambientales anuales de ciudades en países miembros de la OCDE.

**Características principales:**
- `Country`: País
- `City`: Nombre de la ciudad
- `Year`: Año del registro
- `City GDP/Capita`: PIB per cápita (USD)
- `Unemployment %`: Tasa de desempleo (%)
- `Population`: Población urbana
- Otros indicadores ambientales y sociales

**Cardinalidad**: Un registro por ciudad-año

---

## 🛠️ Herramientas y Tecnologías

| Herramienta | Propósito |
|---|---|
| **Python 3.8+** | Lenguaje de programación |
| **Jupyter Notebook** | Ambiente de análisis interactivo |
| **Pandas** | Manipulación y transformación de datos |
| **NumPy** | Operaciones numéricas |
| **Matplotlib** | Visualizaciones estáticas |
| **Seaborn** | Visualizaciones estadísticas avanzadas |

---

## 🔄 Flujo General del Proyecto

### Fase 1: Carga y Exploración
- Importar ambos datasets
- Revisar estructura, tipos de datos y valores faltantes
- Documentar hallazgos iniciales

### Fase 2: Limpieza y Preparación
- Estandarizar nombres de columnas (snake_case)
- Convertir tipos de datos (datetime, float)
- Eliminar duplicados y valores inválidos
- Tratar valores faltantes

### Fase 3: Integración de Datos
- Agregar datos de tráfico por ciudad-año
- Unir (merge) ambos datasets en ciudad y año
- Validar correspondencias entre fuentes

### Fase 4: Análisis Exploratorio (EDA)
- Estadísticas descriptivas
- Distribuciones de variables
- Análisis de correlaciones
- Visualizaciones clave

### Fase 5: Exportación
- Guardar dataset final limpio y procesado
- Exportar reportes de análisis
- Documentar metodología y hallazgos

---

## ⚙️ Detalles Clave de Implementación

### Estandarización de Nombres Geográficos
Los nombres de ciudades y países deben coincidir exactamente entre fuentes para realizar uniones correctas:
- Aplicar `.str.lower()` y `.str.strip()` para normalizar
- Crear tabla de equivalencias para variaciones conocidas
- Validar cardinalidades antes y después de joins

### Agregación de Datos de Tráfico
Dado que TomTom contiene múltiples registros por ciudad:
- Agrupar por `(country, city, year, month)` o `(country, city, year)`
- Calcular métricas: promedio, máximo, mínimo de congestión
- Preservar variabilidad para análisis de volatilidad

### Validación de Calidad
- Verificar que no hay duplicados después de cada transformación
- Confirmar tipos de datos con `.dtypes`
- Validar rangos de valores (ej: congestión 0-100%, desempleo 0-100%)

---

## 📝 Pasos del Análisis (Paso a Paso)

**1. Carga de Datos**
   - Importar `tomtom_traffic.csv` y `oecd_city_economy.csv`
   - Revisar primeras filas y estructura general

**2. Exploración Inicial**
   - Usar `.info()`, `.describe()`, `.value_counts()`
   - Identificar tipos de datos y valores faltantes
   - Documentar hallazgos

**3. Limpieza de Datos**
   - Estandarizar nombres de columnas a snake_case
   - Convertir fechas a datetime
   - Limpiar valores numéricos (remover símbolos, separadores)
   - Eliminar duplicados y filas inconsistentes

**4. Preparación para Unión**
   - Normalizar nombres de ciudades y países
   - Crear año a partir de timestamps
   - Agregar datos de tráfico por ciudad-año

**5. Integración (Merge)**
   - Realizar join de ambos datasets
   - Validar cardinalidad del resultado
   - Confirmar no hay pérdida significativa de datos

**6. Análisis Exploratorio**
   - Correlaciones entre variables
   - Distribuciones por ciudad y región
   - Identificación de valores atípicos

**7. Visualizaciones**
   - Gráficos de dispersión (movilidad vs. productividad)
   - Heatmaps de correlación
   - Mapas o gráficos de clasificación de ciudades

**8. Exportación**
   - Guardar dataset final en CSV
   - Exportar reporte de análisis
   - Documentar metodología

---

## 📦 Instalación y Requisitos

### Prerrequisitos
- Python 3.8 o superior
- pip o conda package manager

### Librerías Requeridas
```bash
pip install pandas numpy matplotlib seaborn jupyter
```

O instalar desde requirements.txt:
```bash
pip install -r requirements.txt
```

---

## 📊 Resultados Esperados

El análisis generará:

1. **Dataset Unificado Limpio**
   - Una tabla con una fila por ciudad-año
   - Todas las variables de movilidad y economía integradas
   - Tipos de datos validados y consistentes

2. **Estadísticas Descriptivas**
   - Distribución de congestión por región
   - Comparativas de productividad económica
   - Correlaciones entre variables

3. **Visualizaciones Clave**
   - Scatter plots mostrando relación movilidad-economía
   - Rankings de ciudades por indicadores combinados
   - Análisis temporal de tendencias

4. **Insights para Decisión**
   - Ciudades prioritarias para inversión
   - Variables más influyentes en desarrollo urbano
   - Recomendaciones de política pública

---

## 📌 Notas Importantes

- El análisis se enfoca en el año **2024** como periodo principal, pero puede extenderse a años anteriores
- Algunos registros pueden no tener correspondencia entre fuentes; esto se documenta en el análisis
- Los datos de TomTom representan congestión en tiempo real; los de OECD son agregaciones anuales
- Validar siempre cardinalidades después de transformaciones para detectar pérdida de datos

---

## 🔗 Referencias Útiles

- [TomTom Traffic Index](https://www.tomtom.com/en_US/traffic-index/)
- [OECD Cities Data](https://www.oecd.org/regional/regional-development/)
- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [Jupyter Notebook Guide](https://jupyter.org/documentation)

