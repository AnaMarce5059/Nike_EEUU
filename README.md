# Dashboard Power BI – Nike (2020–2024)

Este repositorio contiene el análisis comercial de Nike en EE. UU. entre 2020 y 2024, desarrollado en Power BI. Incluye visualizaciones dinámicas, segmentaciones por trimestre, márgenes, campañas y productos destacados.

## 📁 Estructura

| Archivo | Descripción |
|---------|-------------|
| Tablero_NIKE.pbix | Dashboard interactivo |
| Documentacion_Tecnica_Tablero_NIKE.docx | Detalle técnico del modelo |
| MEDIDAS_DAX_NIKE.docx | Medidas DAX utilizadas |
| images/ | Capturas del modelo y reportes |


## 💾 Modelo de Datos

Estructura en estrella con la tabla de hechos `Ventas` y múltiples dimensiones relacionadas.

![Modelo de Datos](images/modelo_datos.png)

## 📐 Medidas DAX

Incluye:
- Facturación Total, Rentabilidad y Margen
- Tasa YoY, Mediana, Cuartiles
- Tooltips con narrativa dinámica

Más detalles en: `MEDIDAS_DAX_NIKE.docx`

## ✅ Conclusión

El tablero permite identificar oportunidades de mejora comercial y analizar la evolución del rendimiento por año, trimestre y categoría.


## 📄 Documentación Técnica

- [Documentación Técnica del Dashboard Nike (2020–2024)](docs/Documentacion_Tecnica_Tablero_NIKE.docx)
- [Medidas DAX utilizadas](MEDIDAS_DAX.md)


## 🎨 Tema personalizado

El diseño visual del dashboard está basado en un archivo `.json` personalizado con colores azules y marrones. Puedes descargarlo y aplicarlo desde Power BI:

📁 [Descargar tema de color (.json)](./themes/Json-marrones-azules.json)
