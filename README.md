# Stats Hub — versión de prueba (solo consulta)

Esta carpeta es un sitio estático listo para publicar. No necesita servidor,
base de datos ni backend: todo corre en el navegador de quien lo visita.

## Qué incluye
- `index.html` — la app completa (Dashboard, Bateo, Pitcheo, Defensa, Comparar, etc.)
- `data/manifest.json` — lista de los partidos que se cargan automáticamente
- `data/*.json` — los archivos de partidos en sí

## Cómo funciona el modo solo-consulta
Al abrir `index.html`, la app lee `data/manifest.json`, descarga cada partido
listado ahí y los carga automáticamente. Los botones de "Cargar JSON(s)",
"Cargar carpeta" y "Limpiar" están ocultos — nadie puede subir ni borrar datos
desde la interfaz pública.

## Cómo agregar un partido nuevo
1. Copia el `.json` del partido dentro de la carpeta `data/`.
2. Abre `data/manifest.json` y agrega el nombre del archivo a la lista, por ejemplo:
   ```json
   [
     "partido_9_American_Beef_vs_Continental_2026-06-27.json",
     "partido_10_Otro_Equipo_vs_Otro_2026-07-04.json"
   ]
   ```
3. Vuelve a subir la carpeta (o solo los dos archivos que cambiaron) a tu hosting.
   No hace falta tocar `index.html`.

## Cómo publicarlo (opciones gratuitas, sin servidor propio)
Cualquiera de estas funciona arrastrando esta misma carpeta:

- **Netlify Drop** (más simple): https://app.netlify.com/drop — arrastras la
  carpeta `deploy/` completa y te da una URL en segundos. Ideal para una fase
  de prueba rápida.
- **GitHub Pages**: subes esta carpeta a un repositorio de GitHub y activas
  Pages en la configuración del repo (Settings → Pages → branch main).
- **Vercel**: similar a Netlify, conecta el repo o arrastra la carpeta.

Importante: el navegador necesita servir los archivos por **http/https**, no
abriendo `index.html` con doble click desde tu computadora (`file://`), porque
la carga automática usa `fetch()` y los navegadores bloquean `fetch` sobre
`file://` por seguridad. Cualquiera de las opciones de arriba resuelve esto
automáticamente.

## Volver al modo de carga manual (para ti, en tu computadora)
Dentro de `index.html`, busca esta línea cerca del final del `<script>`:
```js
const READ_ONLY_MODE = true;
```
Cámbiala a `false`, guarda el archivo y los botones de carga volverán a
aparecer — útil si quieres seguir usando tu copia local para revisar partidos
antes de decidir si los agregas a la versión pública.
