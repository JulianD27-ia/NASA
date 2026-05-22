# 🚀 NASA Explorer

Proyecto desarrollado con Astro que consume la API pública de la NASA para mostrar la Imagen Astronómica del Día (APOD) y un archivo con imágenes recientes.

---

# Descripción

NASA Explorer es un sitio web construido con Astro que obtiene datos científicos reales desde la API oficial de la NASA.

El proyecto incluye:

- Imagen astronómica del día
- Archivo de imágenes recientes
- Diseño espacial moderno
- Fondo animado
- Consumo seguro de API en build time
- Diseño responsive

---

# Tecnologías utilizadas

- Astro
- JavaScript
- HTML5
- CSS3
- NASA APOD API

---

# API utilizada

API oficial de NASA:

https://api.nasa.gov/

Endpoint utilizado:

```txt
https://api.nasa.gov/planetary/apod
```

---

# Estructura del proyecto

```txt
src/
 ├── layouts/
 │    └── Layout.astro
 │
 ├── pages/
 │    ├── index.astro
 │    └── archivo.astro
```

---

# Instalación

Clonar el repositorio:

```bash
git clone https://github.com/TU_USUARIO/nasa-explorer.git
```

Entrar al proyecto:

```bash
cd nasa-explorer
```

Instalar dependencias:

```bash
npm install
```

Ejecutar en desarrollo:

```bash
npm run dev
```

---

# Variables de entorno

Crear un archivo `.env`:

```env
NASA_API_KEY=TU_API_KEY
```

---

# Características principales

## Imagen astronómica del día

Muestra automáticamente la imagen o video publicado por NASA.

## Archivo de imágenes

Lista las imágenes recientes obtenidas desde la API.

## Fetch en build time

Los datos se obtienen durante la construcción del sitio usando Astro.

## Seguridad

La API Key no es visible en el navegador.

---

# Aprendizajes del proyecto

Durante el desarrollo se trabajó con:

- consumo de APIs REST
- renderizado en Astro
- fetch en build time
- rutas y navegación
- manejo de JSON
- manejo de errores
- diseño responsive

---

# Capturas del proyecto

Puedes agregar aquí screenshots del proyecto.

---

# Autor

Proyecto desarrollado por:

- Julian Santiago Tulcán Rodríguez

---

# Despliegue

El proyecto puede desplegarse en:

- Vercel
- Netlify

---

# Licencia

Proyecto educativo sin fines comerciales.

# Reflexión del proyecto

## ¿Qué diferencia hay entre hacer fetch en el frontmatter de Astro y hacerlo en el navegador con JavaScript?

Cuando el fetch se realiza en el frontmatter de Astro, la petición ocurre en el servidor durante la construcción del sitio (build time). Esto permite que los datos ya estén disponibles antes de que la página llegue al navegador del usuario. Además, la API Key permanece protegida porque nunca se expone en el cliente.

En cambio, cuando el fetch se hace desde el navegador usando JavaScript, la petición ocurre después de cargar la página. Esto puede hacer que el sitio sea más lento y también puede exponer la API Key al usuario.

---

## ¿Qué pasa si la API de la NASA cae durante la construcción del sitio? ¿Cómo lo manejas?

Si la API de la NASA falla durante la construcción del sitio, Astro no podrá obtener los datos necesarios y podrían aparecer errores en la página o fallar el build.

Para evitar esto, se implementó manejo de errores usando `try/catch` y verificando `response.ok`. De esta forma se puede mostrar un mensaje alternativo al usuario sin romper completamente el sitio.

Ejemplo:

```js
try {

  const res = await fetch(URL);

  if (!res.ok) {
    throw new Error("Error en la API");
  }

  const data = await res.json();

} catch (error) {

  console.log(error);

}
```

---

## ¿Encontraste algún dato en la respuesta JSON que no esperabas? ¿Cuál y qué significa?

Sí. Uno de los datos más interesantes fue `media_type`.

Este campo indica si el contenido obtenido desde la API es una imagen o un video. Gracias a esto, el proyecto puede decidir automáticamente si mostrar una etiqueta `<img>` o un `<iframe>`.

Ejemplo:

```json
"media_type": "image"
```

o

```json
"media_type": "video"
```

También se encontró el campo `copyright`, que representa el autor de la imagen astronómica. Algunas veces este dato no existe, por lo que se utilizó el operador `??` para mostrar “NASA” como valor por defecto.