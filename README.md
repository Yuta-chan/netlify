# On What Matters
## Blog estático con IA + Netlify

Este blog está desplegado en **Netlify**, que ofrece hospedaje gratuito de sitios estáticos:  
 [https://phenomenal-sopapillas-fd1b5c.netlify.app/](https://phenomenal-sopapillas-fd1b5c.netlify.app/)

La idea es usar **apuntes propios** y **herramientas de IA** para generar páginas en HTML a partir de vídeos de YouTube y sus transcripciones.  
Todo el flujo se apoya únicamente en **HTML + CSS**, sin generadores estáticos ni Docker, buscando la máxima simplicidad.

---

## Herramientas necesarias

- [Netlify](https://www.netlify.com/) — para publicar y hospedar el sitio  
  📺 Tutorial: [Scale & Ship Faster with a Composable Web Architecture | Netlify](https://youtu.be/JT9HMFVCir8)

- [Google NotebookLM](https://notebooklm.google/) — para obtener transcripciones de vídeos o podcasts de YouTube

- [Google AI Studio](https://aistudio.google.com/prompts/new_chat) o [ChatGPT](https://chat.openai.com) — para transformar tus borradores/transcripciones en HTML estructurado siguiendo el estilo del blog

---

## Flujo de trabajo

1. **Escribir borrador**  
   - En tu ordenador, redacta el contenido base de la entrada en `/drafts/` (`.md` o `.txt`).  

2. **Obtener transcripción (opcional)**  
   - En **Google NotebookLM**, crea un nuevo proyecto y pega el enlace del vídeo de YouTube.  
   - Descarga o copia la **transcripción**.

3. **Generar HTML con IA**  
   - Abre **Google AI Studio** (o ChatGPT).  
   - Copia el prompt desde `prompt.md`.  
   - Pega tu borrador o la transcripción.  
   - El modelo devuelve un **HTML completo**, que debe:
     - Cargar los estilos con:  
       ```html
       <link rel="stylesheet" href="/css/site.css">
       ```
     - Incluir navegación mínima:  
       ```html
       <a href="/">Inicio</a> · <a href="/blog/">Blog</a>
       ```

4. **Crear entradas en `/blog/`**  
   - Genera **dos archivos .html**:
     - `/blog/slug.html` → tus apuntes reestructurados.  
     - `/blog/slug_notebooklm.html` → resumen estructurado del vídeo.  

5. **Actualizar índices**  
   - Añade enlaces en `index.html` o en un índice manual dentro de `/blog/`.

6. **Subir cambios y publicar**  
   ```bash
   git add .
   git commit -m "Nueva entrada: slug (+ resumen NotebookLM)"
   git push
   ```
   
Plantilla mínima de entrada
 ```bash
<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>Título de la entrada</title>
  <meta name="description" content="Descripción corta (~160 caracteres)">
  <link rel="stylesheet" href="/css/site.css">
</head>
<body>
  <div class="wrap">
    <header>
      <h1>Título de la entrada</h1>
      <nav><a href="/">Inicio</a> · <a href="/blog/">Blog</a></nav>
      <div class="meta">Publicado: AAAA-MM-DD</div>
    </header>

    <section class="panel">
      <!-- Contenido principal -->
    </section>

    <footer class="panel">
      <div class="meta">© 2025 Judith Urbina</div>
    </footer>
  </div>
</body>
</html>
 ```
🌱 Motivación

Este proyecto surge inspirado en cómo mi padre construyó su web personal con Jekyll y Docker Compose.
Aquí busco una versión simplificada, con tecnologías más accesibles (solo HTML y CSS), y aprovechando las herramientas de IA disponibles en 2025 para automatizar la creación de contenido.

