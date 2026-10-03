# CLAUDE.md

Clon del clásico **Asteroids** en HTML5 Canvas puro. Sin dependencias, sin bundler, sin paso de build.

## Estructura

- `index.html` — página con un `<canvas id="canvas" width="800" height="600">` que carga `game.js`.
- `game.js` — toda la lógica del juego en un solo archivo.
- `favicon.svg` — icono.
- `README.md` — descripción, controles y puntuación.

## Cómo correr

Abrir `index.html` en el navegador, o servir con `npx serve .` y visitar `http://localhost:3000`.
No hay tests ni linter configurados: se verifica jugando en el navegador.

## Arquitectura de `game.js`

- Constantes globales `W`/`H` (800x600) y utilidades: `wrap`, `dist`, `rand`, `randInt`.
- Entrada: objetos `keys` y `justPressed`, consultados con `pressed(code)`.
- Clases: `Bullet`, `Asteroid`, `Ship`, `Particle`.
- Tablas por tamaño de asteroide (índices 1, 2, 3): `RADII`, `SPEEDS`, `POINTS`.
- Estado global: `ship`, `bullets`, `asteroids`, `particles`, `score`, `lives`, `level`, `state` (`'playing' | 'dead' | 'gameover'`).
- Flujo: `initGame()` → `loop(ts)` → `update(dt)` + `draw()`. `nextLevel()`, `killShip()` y `explode()` manejan eventos del juego.
- El espacio es toroidal: las posiciones se envuelven con `wrap`.
- `update(dt)` usa delta time en segundos; no ligar la lógica a los frames.

## Convenciones

- Responder y comentar en español; identificadores de código en inglés, como están.
- JavaScript ES6+ plano (`const`/`let`, clases, funciones flecha), sin módulos ni librerías externas.
- Mantener todo en `game.js` salvo que el archivo crezca demasiado; no introducir bundlers ni dependencias.
- Seguir el estilo existente (2 espacios, punto y coma, comillas simples).

## Notas

- Al cambiar puntuación o controles, actualizar también las tablas del `README.md`.
- Ojo: en `POINTS` el índice 1 es el asteroide pequeño (100) y el 3 el grande (20); el `README` lo lista en orden inverso.
