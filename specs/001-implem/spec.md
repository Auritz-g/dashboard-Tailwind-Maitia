# Especificación 001 — Implementación del dashboard

> **Estado de interfaz:** la implementación muestra datos fuente en tres bloques: Finanzas y audiencia, Productos y Redes. Añade destacados y gráficos únicamente como comparaciones de datos ya proporcionados; no representa el escenario operativo sintético que sigue en esta especificación, el cual se conserva como referencia de decisiones.

## Objetivo

Definir la implementación de un dashboard para una influencer que permita consultar ingresos, productos, métricas de audiencia y rendimiento de sus canales sociales.

## Alcance

El dashboard presentará las métricas proporcionadas en este documento. No se especifican integraciones con APIs, autenticación, persistencia de datos ni edición de métricas; no deben asumirse como parte de esta implementación.

## Datos

### Diccionario de métricas ampliadas y límites de interpretación

Las métricas adicionales de esta ampliación no cuentan con fuentes reales facilitadas. Cualquier cifra de ejemplo que se incorpore a la interfaz se identificará como **Ilustrativo · octubre de 2026**. Este periodo corresponde solo al escenario demostrativo y no se atribuye a las métricas originales.

| Métrica | Definición acordada para la ampliación | Fuente/alcance |
|---|---|---|
| Inscripción | Envío completado del formulario que crea un lead. En el escenario actual, se representa mediante el recuento de leads. | Ilustrativo; octubre de 2026. No equivale a alta de pago ni a suscripción. |
| Usuario activo | Usuario único con al menos una sesión en el periodo. | Ilustrativo; total del escenario, no sumar usuarios entre canales como si fueran únicos. |
| Impresiones | Impresiones brutas reportadas por canales durante el periodo; puede haber repetición de personas y diferencias de medición entre plataformas. | Ilustrativo; desglose por canal. No presentar como alcance único. |
| MRR | Ingreso mensual recurrente de suscripciones activas. | No aplicable con la información disponible: no se ha definido una oferta de suscripción. No calcular a partir de compras puntuales. |
| Interacciones | Suma de likes, comentarios y guardados de la tabla de actividad social ilustrativa. Los compartidos no se incluyen para no mezclar una métrica fuente con el escenario sintético. | Ilustrativo; octubre de 2026; desglosar por canal y no usar como métrica fuente de engagement. El total es 253.300. |
| Churn | Suscripciones activas al inicio del periodo que se dan de baja durante el periodo / suscripciones activas al inicio. | No aplicable hasta que exista y se defina una población de suscripción. |
| Permanencia | Tiempo entre la primera inscripción y la primera compra, expresado como mediana en días. | No disponible como dato fuente. Solo mostrar un valor si se incorpora una cohorte sintética rotulada como ilustrativa; no representa retención de suscriptores. |
| CTR global de campañas (ratio agregado ilustrativo) | Clics ilustrativos de campaña / total de impresiones brutas ilustrativas agregadas por canal del escenario y periodo. | Octubre de 2026: 45.000 / 1.850.000 = 2,43 %. Las impresiones son agregadas entre canales, pueden incluir repeticiones y no están identificadas como impresiones de esos mismos enlaces; por tanto, es un ratio orientativo del escenario y no un CTR estándar comparable. No combinar con el CTR fuente de YouTube. |
| Clics e impresiones sintéticos | 45.000 clics de campaña y 1.850.000 impresiones brutas del escenario. | Ejemplo del mismo periodo; no se atribuye a plataformas individualmente. Las visitas del funnel son sesiones de destino y no se presumen idénticas a clics. |
| Conversión del funnel | Recuento de una etapa / recuento de la etapa inmediatamente anterior; visita→compra también se informa con visitas como denominador. | Escenario ilustrativo; octubre de 2026. Mantener visibles los recuentos y sus etapas. |
| Margen de campaña | (Revenue sintético atribuido a campañas − inversión publicitaria sintética) / revenue sintético atribuido a campañas. | Fórmula posible para margen sobre inversión publicitaria, no margen neto del negocio; excluir costes no proporcionados y etiquetar como ilustrativo. No se muestra un valor hasta separar los ingresos de campaña sintéticos del revenue fuente. |
| Tiempo de conversión | Mediana de días desde el envío del formulario/inscripción hasta la primera compra atribuida. | Solo mostrar para una cohorte ilustrativa con ventana y periodo indicados. |
| Ejemplo de tiempo | Mediana sintética de 4 días, desde formulario hasta compra atribuida. | Demostración ilustrativa; no observado. |
| Attendance rate | Asistentes únicos a un evento en directo / inscripciones completadas para ese mismo evento. | Ejemplo ilustrativo de evento: 162/180 = 90 %; no hay datos fuente de evento. |
| Pass rate | Participantes que cumplen el criterio de aprobación / asistentes que completan la evaluación. | Ejemplo ilustrativo: 122/140 = 87,1 %, con aprobado definido como 70/100 o más; no hay curso fuente definido. |
| Conversión por producto | Conservar los porcentajes de A/B/C como datos facilitados, sin inventar numeradores ni denominadores. | Fuente sin definición de ventana o base. No atribuirles un periodo nuevo. |
| Comisión por producto | Mostrar la tasa indicada del 15 % como condición de comisión; no calcular importes monetarios por producto. | Se desconoce la base contractual y su relación con otras retenciones. |
| ROI/conversiones por producto | No disponible. | Faltan costes, recuentos y revenue atribuibles independientemente a cada producto, más allá de los datos agregados facilitados. |
| ROI de campaña/producto | (Revenue ilustrativo atribuido − inversión ilustrativa) / inversión ilustrativa. | Solo en el escenario sintético, con regla de atribución de último clic en enlace etiquetado dentro de 7 días, una compra atribuida una sola vez y periodo visible. No equiparar con el revenue fuente. |
| Comparativa de plataformas | Poner en paralelo solo métricas cuya definición y periodo sean iguales; las métricas nativas distintas se listan como no equivalentes, no se normalizan ni suman. | Los datos fuente de redes no tienen periodo explícito. El escenario de actividad social se muestra aparte como ilustrativo. |
| Atribución por campaña | Último clic en enlace etiquetado de campaña dentro de 7 días; asignar cada compra a una sola campaña. | Regla sintética para el ejemplo, no método observado en cifras fuente. |
| Productos promocionados | Rutina de otoño: A; Creadoras en directo: B; Selección de favoritos: C. | Asociación inventada para el escenario, no indica ventas fuente atribuidas a esos productos. |
| Revenue de campañas sintético | Rutina de otoño 11.000 €; Creadoras en directo 9.200 €; Selección de favoritos 11.000 €; total independiente 31.200 €. | Reemplaza el total sintético coincidente con la fuente. No es ingreso adicional ni debe sumarse o confundirse con los 42.500 € originales. ROI recalculado sobre estos valores sintéticos. |
| Referencia ilustrativa | CTR de YouTube fuente 2,8 % comparado solo como contexto con umbral fijo de demostración de 3 % (−0,2 puntos porcentuales). | Sin periodo de referencia ni serie histórica, describir como diferencia frente a umbral, no como anomalía o caída temporal. |
| Tops | Campaña: mayor ROI entre tres campañas sintéticas de octubre de 2026. Producto: mayor revenue fuente reportado, periodo sin especificar. | Indicar criterio y universo; no extrapolar rankings a periodos no disponibles. |
| Alertas y tops | Alertas ilustrativas se comparan con el umbral o periodo de referencia que se muestre junto a ellas. Cada ranking indica criterio y universo de comparación. | No afirmar anomalías reales a partir de datos fuente sin una serie temporal comparable. |

No se cuenta con datos reales para las nuevas métricas, ni con costes operativos completos, cohortes, suscripciones, registros de eventos o atribución de campañas. Los valores ilustrativos no rellenan ese vacío como si fueran observaciones reales. Las ganancias netas reportadas (**36.125 €**), el revenue fuente (**42.500 €**) y las retenciones del **15 %** permanecen como conceptos separados y sin recálculo.

La navegación del dashboard usa enlaces HTML estáticos a sus secciones; no hay filtros dinámicos ni recálculo de métricas. No se añade JavaScript propio, de acuerdo con las restricciones del proyecto.

### Escenario operativo ilustrativo (datos ficticios)

Los siguientes valores son contenido sintético de demostración, no datos facilitados ni resultados reales. Se presentan en secciones separadas y con etiquetas visibles «Ilustrativo»; no sustituyen ni recalculan las métricas originales.

| Indicador o etapa | Valor ilustrativo | Consistencia |
|---|---:|---|
| Inscripciones completadas (leads) | 2.700 | Formularios completados; coincide con los leads y representa el 15 % de las visitas. |
| Usuarios activos únicos | 12.400 | Usuarios con al menos una sesión en octubre de 2026; no sumar entre canales. |
| Impresiones brutas | 1.850.000 | Instagram 500.000 + TikTok 1.100.000 + YouTube 250.000; no son personas únicas ni alcance. |
| Interacciones contabilizadas | 253.300 | Suma de likes, comentarios y guardados: Instagram 94.200 + TikTok 138.300 + YouTube 20.800; excluye compartidos. |
| Comparativa de redes | Instagram +18 %, TikTok +32 %, YouTube −2 % | Variaciones originales sin periodo especificado; el resto de métricas se mantiene separado por no ser equivalente entre plataformas. |
| Evento demostrativo | 180 inscripciones, 162 asistentes | Attendance rate de ejemplo: 162/180 = 90 %. No está conectado al embudo comercial. |
| Evaluación demostrativa | 140 completaron, 122 aprobaron | Pass rate de ejemplo: aprobado con al menos 70/100; 122/140 = 87,1 %. |
| Visitas | 18.000 | Base del embudo |
| Leads | 2.700 | 15 % de visitas |
| Leads cualificados | 1.350 | 50 % de leads |
| Inicios de compra | 540 | 40 % de cualificados |
| Compras atribuidas | 250 | 46,3 % de inicios; 1,39 % de visitas |
| Inversión total de campañas | 5.400 € | Suma de las tres campañas |
| Coste por compra | 21,60 € | 5.400 € / 250 compras |
| Ticket medio de campaña | No disponible | No se calcula con el revenue fuente; para mostrarlo hace falta definir revenue de campaña sintético independiente. |
| MRR | No aplicable | No existe una oferta de suscripción definida; no se estima a partir de ventas puntuales. |

| Campaña ficticia | Producto promocionado | Leads | Compras | Revenue sintético independiente | Inversión | ROI ilustrativo |
|---|---:|---:|---:|---:|---:|
| Rutina de otoño | A | 900 | 80 | 11.000 € | 1.800 € | 511 % |
| Creadoras en directo | B | 850 | 70 | 9.200 € | 2.400 € | 283 % |
| Selección de favoritos | C | 950 | 100 | 11.000 € | 1.200 € | 817 % |
| **Total escenario ficticio** | **A, B y C** | **2.700** | **250** | **31.200 €** | **5.400 €** | **478 %** |

ROI = (revenue atribuido − inversión) / inversión. Los **31.200 €** son exclusivamente del escenario sintético independiente y no se suman a ni sustituyen el revenue fuente de **42.500 €**. La atribución es de último clic en enlace etiquetado dentro de 7 días, con compras deduplicadas entre campañas.

| Actividad social ficticia | Publicaciones | Likes | Comentarios | Guardados |
|---|---:|---:|---:|---:|
| Instagram | 8 posts, 12 reels, 20 stories | 84.000 | 4.200 | 6.000 |
| TikTok | 12 vídeos | 125.000 | 3.800 | 9.500 |
| YouTube | 4 vídeos | 18.000 | 1.100 | 1.700 |

Satisfacción ilustrativa: CSAT positivo 94 % (201 de 214 respuestas); NPS +62 (139 promotores, 68 neutros, 7 detractores). Referencia mostrada: CTR fuente de YouTube 2,8 % frente a un umbral fijo ilustrativo de 3 % (−0,2 puntos porcentuales), sin afirmar anomalía temporal. Los rankings se limitan al mayor ROI en las tres campañas sintéticas del periodo octubre de 2026 y, separadamente, a los valores de producto fuente disponibles: Producto A lidera conversión indicada (5,2 %) y Producto B revenue reportado (18.500 €); el periodo de estos datos fuente no está especificado.

### Productos

| Producto | Precio | Revenue atribuido | Tasa de conversión |
|---|---:|---:|---:|
| A | 50 € | 15.200 € | 5,2 % |
| B | 120 € | 18.500 € | 4,1 % |
| C | 80 € | 8.800 € | 3,8 % |

- Hay tres productos: A, B y C.
- La comisión indicada por venta generada es del 15 %.
- Los revenues atribuidos a los productos suman 42.500 €.

### Indicadores generales

- **Total revenue:** 42.500 €.
- **Variación respecto al mes anterior:** +12,5 %.
- **Ganancias netas indicadas:** 36.125 €, presentadas como el dato reportado y sin recalcularlo a partir de las retenciones.
- **Impacto audiencia:** 4,82 %.
- **Engagement promedio:** 7,2 %, con un incremento indicado del 2,1 %.

### Métricas de redes sociales

| Plataforma | Variación indicada | Métricas |
|---|---:|---|
| Instagram | +18 % | 45,2K clics; 1,2K compartidos |
| TikTok | +32 % | 890K visualizaciones; 42 % de finalización |
| YouTube | −2 % | Promedio de visualización: 4 min 12 s; CTR: 2,8 % |

## Requisitos de presentación

- Usar `layout.png`, ubicado en la raíz del proyecto, como referencia visual para la composición y distribución del dashboard. Adaptar la referencia al contenido real, la accesibilidad y el diseño responsive; no es necesario reproducirla literalmente.
- Presentar el total revenue y los ingresos netos como indicadores destacados.
- Presentar la variación del revenue respecto al mes anterior.
- Mostrar el impacto de audiencia y el engagement promedio junto con su variación indicada.
- Mostrar revenue y tasa de conversión por producto.
- Mostrar, por plataforma, su variación y las métricas disponibles.
- La interfaz actual muestra métricas fuente y resúmenes/gráficos comparativos basados únicamente en ellas, dentro de los tres bloques acordados. Las métricas operativas sintéticas documentadas en esta especificación son históricas/de referencia y no deben aparecer en la vista simplificada.
- Presentar las retenciones del 15 % de comisión y 15 % de plataforma dentro del contexto de las ganancias netas, no como tarjetas autónomas. Mostrar 36.125 € como la ganancia neta reportada, sin recalcularla ni combinar las retenciones.
- La navegación principal tiene tres destinos: Finanzas (incluye audiencia), Productos y Redes.
- Cualquier serie de datos de apoyo no presente en los datos originales debe marcarse claramente como ilustrativa.
- Formatear importes en euros y porcentajes con formato español, por ejemplo `42.500 €` y `4,82 %`.
- Diseñar el dashboard con enfoque **mobile-first**: los estilos base deben priorizar pantallas pequeñas y las adaptaciones para pantallas mayores se añaden progresivamente con los breakpoints `sm`, `md` y `lg` de Tailwind CSS v4.
- Construir dimensiones y espaciados con las utilidades de tamaño y espaciado de Tailwind (por ejemplo, `w-*`, `max-w-*`, `min-h-*`, `p-*`, `m-*`, `gap-*`); evitar medidas fijas expresadas en píxeles.
- Proporcionar una estructura responsive que se adapte de forma progresiva a pantallas pequeñas, medianas y grandes.
- Mantener etiquetas y estructura accesibles, con jerarquía clara de encabezados y nombres descriptivos para las métricas y gráficos.

## Requisitos técnicos

- Usar HTML semántico; evitar `<div>` cuando un elemento semántico sea adecuado.
- Usar únicamente Tailwind CSS v4 para los estilos.
- Usar sintaxis y utilidades compatibles con Tailwind CSS v4. No usar instrucciones ni patrones de Tailwind CSS v3.
- No usar `cdn.tailwindcss.com`; mantener la configuración de Tailwind CSS v4 existente o emplear una estrategia de compilación compatible con v4.
- No utilizar tecnologías o frameworks adicionales como React o Vue.
- Escribir las utilidades de Tailwind directamente en el HTML para estilos puntuales.
- Para estilos recurrentes, como tarjetas y badges, definir clases reutilizables en `@layer components` con `@apply`; combinar dichas clases con utilidades en línea para variaciones puntuales.
- No utilizar frameworks.
- No escribir JavaScript propio.
- Implementar gráficos con Charts.css utilizando su estructura basada en tablas y la variable `--size`.
- Incluir una descripción accesible para cada gráfico mediante `caption` o `figcaption`.
- Consultar `AGENTS.md` para las reglas del proyecto.

## Criterios de aceptación

1. El documento HTML tiene una estructura semántica y una jerarquía de encabezados comprensible.
2. Se muestran todos los indicadores generales indicados en esta especificación.
3. Se muestran los tres productos con su precio, revenue atribuido y tasa de conversión.
4. Se muestran las métricas de Instagram, TikTok y YouTube con sus variaciones.
5. Los importes y porcentajes se presentan de forma coherente con el formato español.
6. Los estilos se implementan con Tailwind CSS v4, usando clases reutilizables para patrones recurrentes.
7. Los gráficos se presentan con Charts.css, marcado semántico y una descripción accesible.
8. El diseño se implementa mobile-first y usa `sm`, `md` y `lg` para adaptaciones responsive.
9. Los tamaños y espaciados se expresan con utilidades de Tailwind, sin medidas fijas en píxeles.
10. No se añaden frameworks ni JavaScript propio.

## Decisiones de negocio definitivas y límites

- Comisión del 15 % por venta y retención de plataforma del 15 % son ambas retenciones, pero deben conservarse como conceptos separados; no combinar ni aplicar de nuevo matemáticamente.
- 36.125 € es la ganancia neta indicada y se presenta como reportada, sin recalcularla ni reconciliarla con retenciones.
- No se define el método de cálculo de «Impacto audiencia» ni si el aumento de engagement del 2,1 % representa variación relativa o puntos porcentuales. Mantener los rótulos y valores tal como se proporcionaron.
- No se identifica la métrica concreta ni el periodo de comparación para las variaciones de redes. No inventar explicaciones para ellas.
- No se especifican nombres de marcas o campañas; mostrar métricas por plataforma.
- El periodo visual se indica como ilustrativo; no atribuir las métricas fuente a un mes específico como hecho.
