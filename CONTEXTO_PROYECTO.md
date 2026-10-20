# Contexto del proyecto: dashboard para influencer

> Documento de referencia para futuras conversaciones. Recopila los datos proporcionados y el análisis derivado. Las decisiones definitivas de presentación y estado de implementación se detallan en `specs/001-implem/tasks.md`.

## Objetivo

Construir un dashboard para una influencer con información de productos, ingresos, rendimiento de audiencia y canales de redes sociales. Este documento conserva los datos fuente y sus límites de interpretación.

## Referencia visual

Usar `layout.png`, ubicado en la raíz del proyecto, como referencia visual para la composición y distribución del dashboard. Adaptar el diseño a los datos disponibles, la accesibilidad y las pantallas pequeñas y grandes; no se requiere una copia literal.

## Datos proporcionados

### Productos y comisión

La influencer tiene tres productos:

| Producto | Precio | Comisión por venta indicada |
|---|---:|---:|
| A | 50 € | 15 % |
| B | 120 € | 15 % |
| C | 80 € | 15 % |

La comisión indicada es del **15 % por venta generada**. Decisión posterior definitiva: tanto esta comisión como la retención de plataforma del 15 % se consideran retenciones, y se muestran separadas sin combinarlas ni recalcularlas.

### Métricas generales

- **Total revenue:** 42.500 €.
- **Variación del Total revenue:** incremento del 12,5 % respecto al mes pasado.
- **Ganancias netas indicadas:** 36.125 €. Decisión posterior definitiva: presentarlas como importe neto reportado, sin recalcular ni combinar retenciones en la interfaz.
- **Impacto audiencia:** 4,82 %.
- **Engagement promedio:** 7,2 %, con un incremento del 2,1 %.

### Revenue de productos afiliados principales

| Producto | Revenue | Tasa de conversión |
|---|---:|---:|
| A | 15.200 € | 5,2 % |
| B | 18.500 € | 4,1 % |
| C | 8.800 € | 3,8 % |

### Colaboraciones/métricas por red social

- **Instagram:** crecimiento del 18 %; 45,2K clics y 1,2K compartidos.
- **TikTok:** crecimiento del 32 %; 890K visualizaciones y 42 % de finalización.
- **YouTube:** caída del 2 %; promedio de visualización de 4 min 12 s y CTR del 2,8 %.

No se especificaron nombres de marcas, campañas ni periodos de referencia.

## Alcance actual de la interfaz

Para priorizar claridad y lectura de un vistazo, la interfaz actual conserva tres bloques: **Finanzas y audiencia**, **Productos** y **Redes**. Incluye un breve resumen de los máximos presentes en los datos de productos y redes, y gráficos comparativos accesibles de revenue y conversión por producto. Estas comparaciones reutilizan datos fuente y no son estimaciones. No presenta el escenario operativo sintético ni métricas calculadas. Las cifras sintéticas descritas en `specs/001-implem/spec.md` se conservan como referencia documental, no como datos visibles del dashboard. El revenue fuente permanece en **42.500 €** y la ganancia neta reportada en **36.125 €**.

Las cifras originales siguen sin modificarse. No se agregan MRR, churn ni permanencia, porque no se ha definido una oferta de suscripción.

## Cálculos derivados (no usar para recalcular en la interfaz)

Estos cálculos se basan en los datos proporcionados y son análisis aritmético, no cifras para reconstruir o sustituir las ganancias netas definitivas mostradas en el dashboard:

1. Los revenues de A, B y C suman **42.500 €**: 15.200 € + 18.500 € + 8.800 €. Coinciden con el Total revenue.
2. El 15 % de 42.500 € es **6.375 €**. El 85 % restante es **36.125 €**, por lo que la cifra de Ingresos cuadra aritméticamente con una tasa de plataforma del 15 % aplicada al Total revenue.
3. Si el crecimiento del 12,5 % compara el Total revenue actual con el del mes anterior, el revenue anterior sería aproximadamente **37.777,78 €** (42.500 € ÷ 1,125).
4. Si la comisión del 15 % se aplica directamente al revenue atribuido a cada producto, las comisiones serían:
   - A: **2.280 €**.
   - B: **2.775 €**.
   - C: **1.320 €**.
   - Total: **6.375 €**.
   Esta aplicación es condicional: no está confirmado si la comisión se calcula sobre estos revenues ni cómo interactúa con la tasa de plataforma.
5. Dividir el revenue por el precio da una cantidad implícita de unidades: A = **304**, B = **154,17** y C = **110**. El valor de B no es un número entero; conviene confirmar si el precio es fijo y si el revenue incluye redondeos, descuentos, devoluciones u otros ajustes.
6. El incremento del engagement es ambiguo:
   - Si es un aumento **relativo** del 2,1 %, el valor anterior estimado sería aproximadamente **7,05 %** (7,2 % ÷ 1,021).
   - Si significa un aumento de **2,1 puntos porcentuales**, el valor anterior sería **5,1 %**.

## Aclaraciones y límites de interpretación

- La comisión y la retención de plataforma se conservan separadas; no inferir otra relación ni realizar cálculos de interfaz.
- ¿Los revenues por producto son importes brutos? ¿Pueden incluir descuentos, devoluciones, impuestos, redondeos o ajustes?
- ¿El precio publicado de cada producto es fijo y en euros?
- ¿Cómo se define y calcula “Impacto audiencia” (4,82 %)?
- ¿El aumento del engagement del 2,1 % es relativo o de 2,1 puntos porcentuales?
- ¿A qué periodo se refieren los cambios de Instagram (+18 %), TikTok (+32 %) y YouTube (−2 %)?
- ¿Qué significa “Recent brand collaborations” en este contexto: se añadirán marcas/campañas, o las cifras indicadas son las métricas disponibles por plataforma?

## Visualizaciones del dashboard

El dashboard utiliza gráficos solo cuando existe una comparación real útil entre categorías, como revenue y conversión por producto. No añadir series semanales ficticias ni gráficos de una sola métrica que no permitan comparar datos.
