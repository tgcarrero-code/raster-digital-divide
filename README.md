# Raster Digital Divide — Análisis de Brecha Digital Territorial en Cusco

## Descripción y pregunta analítica
Este proyecto construye un pipeline de análisis raster geoespacial para medir la brecha digital territorial en la región Cusco, Perú, cruzando datos satelitales de luz nocturna NASA (proxy de urbanización) con densidad de cobertura de red móvil OSIPTEL (proxy de acceso a internet). La pregunta central es: ¿qué distritos de Cusco presentan mayor exclusión digital y por qué?

## Datasets utilizados
- `VNL_cusco_2025.tif` — NASA Black Marble nighttime radiance 2025 (EPSG:4326)
- `kernel_cobmovil2019_50m.tif` — Cobertura móvil OSIPTEL 2019, kernel 50m (EPSG:32719)

Ambos disponibles en el repositorio del curso: `Data-Science-Python/_data/Raster_2026/`

## Pipeline de análisis
1. **Step 0** — Instalación e importación de librerías
2. **Step 1** — Carga e inspección de rasters
3. **Step 2** — Reproyección de conectividad a EPSG:4326 y alineación al grid del VNL
4. **Step 3** — Normalización robusta por percentil 2-98
5. **Step 4** — Mapa 1: VNL raw vs normalizado
6. **Step 5** — Mapa 2: IBD y EDT con interpretación
7. **Step 6** — Mapa 3: Niveles de prioridad de intervención
8. **Step 7** — Mapa 4: Riesgo de exclusión social con filtro gaussiano
9. **Step 8** — Clasificación territorial 2x2 exportada como GeoTIFF
10. **Step 9** — Resumen estadístico, correlación y Welch t-test
11. **Step 10** — Exportación de GeoTIFFs y dashboard final

## Instalación
```bash
pip install rasterio numpy matplotlib scipy seaborn pandas
```

## Cómo correr el notebook
1. Descarga los archivos `.tif` del repositorio del curso y colócalos en `data/`
2. Abre `notebooks/digital_divide_cusco.ipynb` en Google Colab
3. Ejecuta todas las celdas en orden

## Descripción de outputs
| Archivo | Descripción |
|---|---|
| `vnl_norm.tif` | VNL normalizado [0-1] |
| `conn_norm.tif` | Conectividad normalizada [0-1] |
| `ibd_brecha_digital.tif` | Índice de Brecha Digital [-1, 1] |
| `clasificacion_brecha.tif` | Clasificación 2x2 en 4 clases |
| `dashboard_brecha_digital.png` | Dashboard final a 150 dpi |

## Principales hallazgos
La ciudad de Cusco y el corredor Urubamba-Quillabamba concentran la mayor actividad nocturna pero también muestran zonas con brecha digital activa. El 90% del territorio regional corresponde a Brecha Crítica — zonas sin luz ni conectividad. Solo el 1.7% es urbano conectado, evidenciando una profunda desigualdad digital territorial.

## Limitaciones
- La cobertura móvil es de 2019 y puede no reflejar la situación actual
- El VNL incluye fuentes de luz no antrópicas en algunos píxeles
- La resolución del kernel limita el detalle en zonas rurales dispersas
