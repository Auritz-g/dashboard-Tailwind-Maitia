# Reglas del proyecto: dashboard para influencer

Consulta `CONTEXTO_PROYECTO.md` para los datos y el análisis del dashboard.
Usa `layout.png`, ubicado en la raíz del proyecto, como referencia visual para la composición y distribución del dashboard. Síguelo como guía, adaptándolo a los datos, la accesibilidad y el diseño responsive; no lo interpretes como una imagen que haya que reproducir literalmente.

## HTML

- Usa HTML semántico para que el documento tenga una estructura clara: `header`, `nav`, `main`, `section`, `article`, `aside`, `footer`, `h1`–`h6`, `ul`/`ol`, `dl`, `table`, `figure`/`figcaption`, `data` y `time`.
- Respeta una jerarquía de encabezados coherente: un solo `h1` y ningún nivel omitido.
- Usa `<div>` solo cuando no exista un elemento semántico adecuado y sea imprescindible para el diseño.

## Estilos

- Aplica los estilos únicamente con **Tailwind CSS v4**.
- Por defecto, escribe los estilos con clases de utilidad de Tailwind directamente en el HTML (`class="..."`).
- Crea una clase de componente cuando un mismo conjunto de utilidades se repita en varios elementos (tarjetas, badges, encabezados de sección, contenedores de gráficos, etc.).
- Define esas clases en `@layer components` dentro de `<style type="text/tailwindcss">`, usando `@apply` con utilidades de Tailwind. Usa `@utility` solo para utilidades sencillas que deban funcionar con variantes (`hover:`, `md:`, etc.).
- Las clases de componente contienen solo el estilo base común. Los ajustes puntuales de cada elemento se añaden en línea junto a la clase: `class="card md:col-span-2"`.
- No escribas CSS personalizado fuera de las capacidades de Tailwind v4 (`@theme`, `@utility`, `@layer components`, `@apply`).

## Restricciones

- No uses frameworks: ni de JavaScript (React, Vue, Alpine, etc.) ni de CSS distintos de Tailwind.
- No escribas JavaScript propio. La única excepción es el script de Tailwind CSS v4 para navegador (`@tailwindcss/browser@4`) ya incluido en `index.html`.

## Gráficos

- Crea los gráficos con **Charts.css** (`https://cdn.jsdelivr.net/npm/charts.css/dist/charts.min.css`), usando su marcado basado en `<table>` y la variable `--size`.
- Acompaña cada gráfico de un `<caption>` o `figcaption` descriptivo para mantener la accesibilidad.
