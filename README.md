# Dashboard Power BI – Nike (2020–2024)

Este repositorio contiene el análisis comercial de Nike en EE. UU. entre 2020 y 2024, desarrollado en Power BI. Incluye visualizaciones dinámicas, segmentaciones por trimestre, márgenes, campañas y productos destacados.

## 📁 Estructura

📁 Publicar en Github
├── venv/
├── Tablero_NIKE.pbix
├── Documentacion_Tecnica_Tablero_NIKE.docx
├── MEDIDAS_DAX_NIKE.docx
├── README.md
├── requirements.txt         ← si usás Python
├── images/
│   ├── modelo_datos.png
│   └── estructura_medidas.png


## 📐 Modelo de Datos

Estructura en estrella con la tabla de hechos `Ventas` y múltiples dimensiones relacionadas.

![Modelo de Datos](images/modelo_datos.png)

## 🧠 Medidas DAX

Incluye:
- Facturación Total, Rentabilidad y Margen
- Tasa YoY, Mediana, Cuartiles
- Tooltips con narrativa dinámica

Más detalles en: `MEDIDAS_DAX_NIKE.docx`

## ✅ Conclusión

El tablero permite identificar oportunidades de mejora comercial y analizar la evolución del rendimiento por año, trimestre y categoría.
