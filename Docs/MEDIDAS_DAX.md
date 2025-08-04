
# 📊 Medidas DAX – Tablero Power BI Nike (2020–2024)

Este documento describe las medidas DAX utilizadas en el proyecto, organizadas por carpeta funcional según su ubicación en Power BI.

---

## 📁 Análisis Gral.

### 🔸 Calificación Crecimiento
```dax
VAR Estrella = UNICHAR(11088)
VAR Crecimiento = 
    VAR Ventas_Actuales = [Facturación Total]
    VAR Ventas_Anteriores = CALCULATE([Facturación Total], DATEADD('CALENDARIO'[Fecha], -1, QUARTER))
    RETURN DIVIDE(Ventas_Actuales - Ventas_Anteriores, Ventas_Anteriores)

RETURN
SWITCH(TRUE(),
    Crecimiento <= 0, REPT(Estrella, 1),
    Crecimiento <= 0.05, REPT(Estrella, 2),
    Crecimiento <= 0.15, REPT(Estrella, 3),
    Crecimiento <= 0.30, REPT(Estrella, 4),
    REPT(Estrella, 5))
```

### 🔸 Facturación promedio
```dax
AVERAGE(Ventas[Total Facturado])
```

### 🔸 Facturación Total
```dax
SUM(Ventas[Total Facturado])
```

### 🔸 Margen Alto (%)
```dax
CALCULATE(
    COUNTROWS(Ventas),
    Ventas[Margen_Evaluado] = "Margen Alto"
) / COUNTROWS(Ventas)
```

### 🔸 Margen Bajo (%)
```dax
CALCULATE(
    COUNTROWS(Ventas),
    Ventas[Margen_Evaluado] = "Margen Bajo"
) / COUNTROWS(Ventas)
```

### 🔸 Margen Medio (%)
```dax
CALCULATE(
    COUNTROWS(Ventas),
    Ventas[Margen_Evaluado] = "Margen Medio"
) / COUNTROWS(Ventas)
```

### 🔸 Margen Operativo
```dax
SUM(Ventas[Margen Operativo])
```

### 🔸 Rentabilidad
```dax
SUM(Ventas[Rentabilidad ($) ])
```

### 🔸 Rentabilidad promedio
```dax
AVERAGE(Ventas[Rentabilidad ($) ])
```

### 🔸 Tasa Facturación YoY
```dax
VAR __PREV_YEAR = CALCULATE([Facturación Total], DATEADD('CALENDARIO'[Fecha], -1, YEAR))
RETURN IF(
    NOT(ISBLANK(__PREV_YEAR)),
    DIVIDE([Facturación Total] - __PREV_YEAR, __PREV_YEAR),
    BLANK()
)
```

### 🔸 Ventas
```dax
COUNTROWS(Ventas)
```

---

## 📁 Comportamiento comercial

### 🔸 Evaluación Tasa
```dax
VAR Zapatilla = UNICHAR(128095)
VAR __PREV_MONTH = CALCULATE([Facturación Total], DATEADD('Calendario'[Fecha], -1, MONTH))
VAR __VARIACION = DIVIDE([Facturación Total] - __PREV_MONTH, __PREV_MONTH, 0)
RETURN IF(SELECTEDVALUE(CALENDARIO[Mes]) IN VALUES(CALENDARIO[Mes]),
    SWITCH(TRUE(),
        __VARIACION < 0, REPT(Zapatilla, 1),
        __VARIACION <= 0.05, REPT(Zapatilla, 2),
        __VARIACION <= 0.10, REPT(Zapatilla, 3),
        __VARIACION <= 0.20, REPT(Zapatilla, 4),
        REPT(Zapatilla, 5)
    ),
    BLANK()
)
```

### 🔸 Mensaje_Resumen
```dax
"Explore los productos más rentables, campañas más efectivas y el comportamiento mensual en el año " &
SELECTEDVALUE('Calendario'[Año])
```

---

## 📁 Conclusión

### 🔸 Flechas
```dax
IF ([Tasa Facturación YoY] < 0,
    "https://cdn-icons-png.flaticon.com/128/14034/14034448.png",
    "https://cdn-icons-png.flaticon.com/128/14024/14024979.png")
```

### 🔸 Limite Tacometro
```dax
MAX('Rentabilidad anual por mes'[Rentabilidad mensual])
```

### 🔸 Mediana
```dax
PERCENTILE.INC(Ventas[Rentabilidad ($) ], 0.50)
```

### 🔸 Primer Cuartil
```dax
PERCENTILE.INC(Ventas[Rentabilidad ($) ], 0.25)
```

### 🔸 Tercer Cuartil
```dax
PERCENTILE.INC(Ventas[Rentabilidad ($) ], 0.75)
```

---

## 📁 Portada

### 🔸 Ultima_Actualizacion
```dax
FORMAT(NOW(), "dd/mm/yyyy HH:MM:SS")
```

---

## 📁 Tooltips

### 🔸 Narrativa Tooltip
```dax

```
Narrativa Tooltip = 
VAR Texto1 = "Usted se ha posicionado en el estado de "
VAR Texto2 = ". El total facturado por las ventas realizadas en este estado fue de "
VAR Texto3 = ", por un total de "
VAR Texto4 = " ventas efectuadas."
VAR Texto5 = " El producto más vendido en este estado fue: "
VAR Texto6 = ", con "
VAR Texto7 = " unidades vendidas, generando un total de "

VAR Estado = SELECTEDVALUE(Estado[State])

VAR Facturacion = FORMAT([Facturación Total], "$ #,###")
VAR CantidadVentas = FORMAT([Ventas], "#,###")

VAR TablaProductos =
    ADDCOLUMNS(
        VALUES(Nombre_Producto[PRODUCT_NAME]),
        "Unidades", CALCULATE(SUM(Ventas[Unidades Vendidas])),
        "Facturacion", CALCULATE(SUM(Ventas[Total Facturado]))
    )

VAR ProductoTop =
    TOPN(1, TablaProductos, [Unidades], DESC)

VAR NombreProducto = SELECTCOLUMNS(ProductoTop, "Producto", Nombre_Producto[PRODUCT_NAME])
VAR UnidadesVendidas = SELECTCOLUMNS(ProductoTop, "Unidades", [Unidades])
VAR FacturacionProducto = SELECTCOLUMNS(ProductoTop, "Facturacion", [Facturacion])

RETURN
    Texto1 & Estado & 
    Texto2 & Facturacion &
    Texto3 & CantidadVentas &
    Texto4 &
    Texto5 & NombreProducto &
    Texto6 & FORMAT(UnidadesVendidas, "#,###") &
    Texto7 & FORMAT(FacturacionProducto, "$ #,###") & "."


---

## 📁 Análisis de eficiencia

### 🔸 Análisis de eficiencia
```dax
{
    ("Margen Bajo (%)", NAMEOF('Tabla Medidas'[Margen Bajo (%)]), 0),
    ("Margen Medio (%)", NAMEOF('Tabla Medidas'[Margen Medio (%)]), 1),
    ("Margen Alto (%)", NAMEOF('Tabla Medidas'[Margen Alto (%)]), 2)
}
```
