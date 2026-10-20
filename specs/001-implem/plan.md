# Plan de implementación del dashboard financiero

El plan se basa en `specs/001-implem/spec.md`, `CONTEXTO_PROYECTO.md` y las reglas de `AGENTS.md`.

## 1. Objetivo de diseño

Diseñar el dashboard para que, de un vistazo, las métricas prioritarias se entiendan sin ambigüedad. La jerarquía debe destacar primero Total revenue (**42.500 €**) y ganancias netas reportadas (**36.125 €**); después mostrar la variación de revenue, audiencia/engagement, comparativa de productos y métricas de redes. Cada dato tendrá una etiqueta clara, unidades visibles y contexto breve cuando sea necesario.

No añadir elementos decorativos, periodos supuestos ni visualizaciones que no respondan a una pregunta de comparación concreta. Retirar series semanales ficticias y cualquier gráfico que no compare datos reales proporcionados. Mantener Charts.css solo para las comparativas reales por producto (revenue y conversión), cada una en una escala separada y con su caption accesible. Los demás valores se presentan como métricas numéricas.

## 2. Decisiones de negocio y fidelidad

- Los 36.125 € son las ganancias netas indicadas y se presentan como importe reportado; no recalcularlas.
- La comisión por venta del 15 % y la retención de plataforma del 15 % se mantienen separadas y claramente etiquetadas, sin sumarlas ni aplicarlas otra vez.
- No inferir periodos o bases de comparación que no se proporcionaron para las variaciones.
- Conservar los datos de producto, audiencia y redes en sus valores originales. No agregar cifras ficticias al dashboard.

## 3. Estructura y lectura rápida

Mantener una navegación de tres destinos: **Finanzas** (incluye audiencia), **Productos** y **Redes**. El orden de contenido será:

1. Resumen financiero con Total revenue y ganancias netas como indicadores visuales principales; retenciones explicativas junto al neto, no como tarjetas autónomas.
2. Impacto de audiencia y engagement como indicadores simples.
3. Tabla concisa de productos con precio, revenue y conversión, seguida de dos comparativas Charts.css accesibles que no dupliquen datos nuevos ni alteren los valores.
4. Tarjetas simples de Instagram, TikTok y YouTube con las métricas facilitadas.

Usar títulos y etiquetas descriptivos, formato numérico español y texto explícito para las variaciones; no depender del color para expresar significado. Mantener estructura HTML semántica y jerarquía de encabezados lógica.

## 4. Diseño mobile-first y sistema visual

- Empezar por una columna legible en móvil; ampliar progresivamente a dos o tres columnas cuando el ancho lo permita, con variantes `sm:`, `md:` y `lg:` de Tailwind CSS v4.
- Asegurar que las cifras críticas se ven antes que el contenido secundario y que las tablas pueden consultarse en pantallas estrechas sin deformarse.
- Usar una paleta pastel de bajo ruido visual: fondo claro y superficies suaves, con magenta pastel como color distintivo de la influencer y tonos complementarios discretos. Mantener contraste suficiente para texto, foco y controles.
- Aplicar movimiento y ornamentación con moderación; respetar `prefers-reduced-motion`.
- Construir dimensiones y espaciados con utilidades Tailwind, evitando medidas fijas en píxeles.

## 5. SEO y metadatos

- Mantener `lang="es"`, título específico y conciso, descripción meta única que resuma el contenido real, viewport y theme color coherentes con la paleta.
- Mantener un solo `h1`, encabezados de sección jerárquicos, contenido textual indexable y enlaces internos con nombres comprensibles.
- Usar marcado semántico y datos estructurados accesibles; no añadir keywords repetidas, contenido oculto para SEO ni metadatos sociales con valores inventados.
- Evitar JavaScript propio, frameworks y dependencias innecesarias; mantener Tailwind CSS v4 y Charts.css de acuerdo con las reglas existentes.

## 6. Validación

Antes de cerrar la implementación, revisar navegación y destinos, cifras frente a las fuentes, concordancia entre la tabla de productos y sus dos gráficos, etiquetas y accesibilidad, legibilidad mobile-first, contraste de la paleta pastel, preferencias de movimiento y metadatos SEO. Confirmar que no hay series ficticias ni gráficos innecesarios, frameworks, JavaScript propio, `cdn.tailwindcss.com`, patrones Tailwind v3 o medidas fijas en píxeles.

## 7. Nueva fase: ampliar métricas operativas pendientes

Esta sección recoge una fase operativa anterior. Sus métricas sintéticas se conservan como referencia, pero fueron retiradas de la interfaz en una simplificación posterior. El dashboard actual prioriza datos fuente y conserva sin cambios la estructura de tres bloques (Finanzas y audiencia, Productos y Redes); se permiten resúmenes comparativos o gráficos que se limiten a visualizar esos mismos datos sin inferencias adicionales. No volver a incorporar bloques sintéticos sin una solicitud explícita.

### 7.1 Criterios de fidelidad y datos

- Conservar sin cambios las cifras fuente: revenue **42.500 €**, ganancias netas reportadas **36.125 €**, las retenciones separadas del **15 %** por venta y del **15 %** de plataforma, productos A/B/C y métricas originales de Instagram, TikTok y YouTube.
- No recalcular las ganancias netas, combinar las retenciones ni presentar cálculos condicionales como cifras reales.
- Se permiten datos sintéticos adicionales si cada bloque y visualización que los use se identifica de forma visible como **Ilustrativo**. Mantener consistencia interna entre KPI, tablas y funnel, sin hacer pasar esos valores por resultados fuente.
- Resuelto en la implementación: el escenario sintético de campañas suma **31.200 €**, está etiquetado como independiente y se aclara que no forma parte de los **42.500 €** de revenue fuente. No cambiar el dato fuente.

### 7.2 Métricas y secciones a completar

1. **Volumen:** añadir inscripciones, usuarios activos e impresiones. Antes de elegir etiquetas y fórmulas, definir qué evento cuenta como inscripción, qué ventana determina un usuario activo y si las impresiones son brutas, únicas o por canal. Mostrar periodo y fuente de cada valor.
2. **Ingresos:** añadir MRR solo si se confirma que existe una oferta de suscripción y se define qué ingresos recurrentes se incluyen. Hacer explícitos el periodo y el significado de ventas/revenue y ganancias netas; mostrar por separado las dos retenciones sin reconstruir importes ni atribuir al dashboard cálculos no confirmados.
3. **Engagement:** incorporar un total explícito de interacciones y especificar qué acciones lo componen. Si se agregan plataformas, hacer visible el alcance y evitar sumar métricas incompatibles.
4. **Retención:** incorporar churn y permanencia únicamente cuando se definan población, periodo, evento de baja y método de duración (por ejemplo, media, mediana o cohortes). Si no hay suscripción o seguimiento de cohortes, señalarlas como no disponibles/no aplicables, o usar un ejemplo claramente ilustrativo sin sugerir que es un dato real.
5. **Rendimiento:** añadir CTR global y tasas por etapa del funnel, indicando numerador, denominador y periodo. Elegir una única base de CTR (clics/impresiones o clics/alcance) y no mezclarla entre secciones. Mantener recuentos junto a las tasas cuando ayuden a interpretarlas.
6. **Eficiencia:** añadir margen solo después de definir ingresos y costes incluidos, nivel de agregación y periodo. Añadir tiempos de conversión/respuesta con hitos inicial/final y estadístico (media o mediana).
7. **Drivers:** añadir attendance rate y pass rate tras definir asistentes frente a inscritos y el criterio de aprobado. Completar por producto comisiones, conversiones y ROI únicamente con bases acordadas (ingreso atribuible, inversión y periodo); mantener cada retención identificada por separado.
8. **Comparativa de plataformas:** crear una tabla con definiciones y ventanas temporales homogéneas para Instagram, TikTok y YouTube. No forzar equivalencias entre métricas nativas no comparables: separarlas y anotar las diferencias.
9. **Operaciones y campañas:** identificar los productos promocionados por campaña y sus reglas de atribución; definir un periodo/benchmark y umbrales para alertas de anomalía, pico o caída; y añadir listados de mejores resultados con criterio y periodo seleccionables o claramente rotulados.

### 7.3 Interacción y restricciones técnicas

No implementar filtros dinámicos de fecha, plataforma o producto con JavaScript mientras siga vigente la prohibición de JavaScript propio. Se pueden proporcionar opciones estáticas, enlaces internos o vistas predefinidas. Si se requieren filtros que recalculen tarjetas y tablas en tiempo real, será necesario aprobar expresamente un cambio de esa restricción antes de implementarlos.

### 7.4 Validación de la nueva fase

Verificar definiciones, unidades, periodo, fuente y carácter ilustrativo junto a cada métrica nueva; comprobar consistencia de tablas, KPIs, funnel y campañas; revisar que ninguna cifra nueva se confunda con revenue o ganancias fuente; y validar accesibilidad, mobile-first y restricciones técnicas con los criterios de la sección 6. El desglose ejecutable y el estado de cada trabajo se mantienen en `tasks.md`.
