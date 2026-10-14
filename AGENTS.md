# AGENTS.md

## Proyecto

Sitio HTML autocontenido (`index.html`) — línea del tiempo eschatológica interactiva con 22 eventos bíblicos en secciones de pantalla completa, desde el Calvario hasta la Nueva Jerusalén.

## Estructura

- **Un solo archivo**: `index.html` contiene todo (HTML + CSS + JS). No hay build step ni dependencias externas salvo Google Fonts.
- **Datos**: array `EVENTS` en el `<script>` — cada evento tiene id, título, cuándo, lugar, a quién afecta, cita, **texto bíblico completo** (`verse`), descripción y tipo de escena SVG.
- **Navegación por ubicación**: sidebar fijo (desktop) / barra inferior (mobile). Cada ubicación tiene su propio tema de color vía `body[data-location]` y CSS custom properties.
- **Pantalla completa**: cada evento es una `<section>` de 100vh con scroll-snap, fondo SVG generado, overlay y contenido centrado.
- **Fondos SVG**: 22 escenas únicas generadas por funciones en el objeto `SCENES` — cada una con cielo gradiente, elementos atmosféricos (estrellas, nubes, rayos de luz, niebla) y el sujeto principal.
- **Parallax**: canvas de estrellas + orbes CSS + parallax de fondo por escena (translateY basado en posición del viewport).
- **Animaciones**: IntersectionObserver con stagger children, entrada cubic-bezier, hover effects en citas.

## Comandos

No hay comandos. Es un archivo estático — se abre directamente en el navegador o se sirve con cualquier server estático:

```bash
# Opcional: sirve localmente
python3 -m http.server 8000
# Luego abre http://localhost:8000
```

## Decisiones de diseño

- **SVG inline** por evento (no imágenes externas) — autocontenido, escalable, hereda `currentColor` para temas.
- **Temas por ubicación**: Calvario (rojo), Tierra (ámbar), Jerusalén (dorado), Cielo (azul), Meguido (rojo oscuro), Abismo (violeta), Nueva Tierra (verde dorado).
- **Fuentes**: Cinzel (títulos), EB Garamond (cuerpo), Inter (UI).
- **Sin frameworks** — vanilla JS para mantener el archivo único y portable.
- **Citas bíblicas**: texto completo de cada versículo en un componente `.verse-box` con borde izquierdo dorado, itálica y hover con glow.

## Responsive

- Desktop: timeline con línea central y cards alternados.
- Mobile (<768px): línea a la izquierda, cards a la derecha, nav inferior horizontal.
- Breakpoints: 768px, 480px, 360px con ajustes progresivos de tipografía y espaciado.

## Accesibilidad

- `prefers-reduced-motion` respeta la configuración del sistema.
- Contraste de texto verificado para ambos temas (claro sobre oscuro).
- Navegación por teclado en los filtros (botones nativos).
