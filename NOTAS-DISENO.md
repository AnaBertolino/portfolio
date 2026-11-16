# Notas de diseño — portfolio de Ana

Estas notas están para que entiendas **cómo funciona** tu página, sin tener que escribir código. Leelas una vez entera y después usalas como consulta.

## 1. La idea general: una web es un conjunto de archivos

Tu sitio es "estático": son archivos de texto que el navegador lee y dibuja. No hay base de datos ni servidor propio. GitHub Pages simplemente le entrega esos archivos a quien visita anabertolino.com. Por eso es gratis y simple.

| Archivo | Qué es | Analogía |
|---|---|---|
| `index.html` | Qué contenido hay (títulos, textos, tarjetas) y en qué orden | El **esqueleto** |
| `css/styles.css` | Cómo se ve (colores, tamaños, espacios) | La **piel y la ropa** |
| `assets/` | Imágenes (por ahora vacía; acá va `profile.jpg`) | El **álbum de fotos** |
| `CNAME` | Le dice a GitHub Pages que el sitio vive en anabertolino.com | **No lo toques**: si lo borrás o cambiás, se cae el dominio |
| `NOTAS-DISENO.md` | Este archivo | — |

Separar contenido (HTML) y aspecto (CSS) es a propósito: podés cambiar toda la paleta sin tocar un solo texto, y al revés.

## 2. Cómo cambiar la paleta de colores

Una **variable CSS** es un nombre que le ponés a un valor para usarlo en muchos lugares. Por ejemplo, `--color-accent-dark: #3d5e46;` significa "el verde oscuro es #3d5e46". Después, en el resto del archivo, se escribe `var(--color-accent-dark)` en vez del código del color. Si cambiás el valor una vez, cambia en toda la página.

Abrí `css/styles.css`: las primeras ~35 líneas son el bloque `:root { ... }`. Ahí están todos los colores, cada uno con un comentario que explica qué controla:

- `--color-bg`: fondo general (crema)
- `--color-surface`: fondo de tarjetas y header
- `--color-text` y `--color-text-muted`: texto principal y secundario
- `--color-accent`, `--color-accent-dark`, `--color-accent-soft`: la familia sage green
- `--color-on-accent`: color del texto sobre los botones oscuros
- `--color-pop` y `--color-pop-soft`: el "pop" terracota (subrayado del nombre, borde de los borradores, tarjeta de la tesis)
- `--color-border`: líneas finitas
- `--color-shadow`: sombra de las tarjetas

Para probar otra paleta: cambiá el código hexadecimal (el `#xxxxxx`) de una línea, guardá, y Live Server recarga la página solo. Tip: buscá "color picker" en Google para elegir colores. **Ojo con el contraste**: el texto tiene que distinguirse bien del fondo (los textos tienen que quedar oscuros sobre fondos claros); si cambiás `--color-accent-dark` o `--color-text-muted`, mantenelos bastante oscuros.

Más abajo en `:root` hay también variables de tipografía (`--font-body`, `--font-heading`, `--font-size-base`) y espaciado (`--space-*`, `--radius`). Misma idea.

**Regla que respeté:** no hay ningún color escrito fuera de `:root`. Si agregás algo nuevo, creá una variable en vez de pegar un código de color suelto.

## 3. Cómo editar textos y agregar un proyecto

- **Editar un texto:** abrí `index.html`, buscá el texto (Ctrl+F) y cambialo. Lo que está entre `<p>` y `</p>` es un párrafo; no borres los `<` `>`.
- **Agregar un proyecto:** en la sección Projects, copiá un bloque entero desde `<article class="card">` hasta su `</article>`, pegalo justo debajo del último, y cambiá título, descripción y etiquetas. La grilla se acomoda sola.
- **Los comentarios** `<!-- así -->` no se ven en la página: son notas para vos.

## 4. Placeholders (borradores) pendientes

Todo texto borrador tiene la clase `placeholder`, que le dibuja una **línea punteada terracota** a la izquierda para que lo veas enseguida. Cuando completes un texto, borrá `placeholder` del `class` de ese párrafo (por ejemplo `<p class="placeholder">` → `<p>`).

Pendientes, todos en `index.html`:

1. **Hero**: revisar la frase de posicionamiento (párrafo con `class="lead placeholder"`).
2. **Proyecto 1, Technical Troubleshooting Agent**: descripción, Role y Tools (marcados TODO).
3. **Proyecto 2, Support Documentation Agent**: descripción, Role y Tools.
4. **Proyecto 3, New PC Inventory — Project Management**: descripción, Role y Tools.
5. **Proyecto 4, tesis UWB**: revisar la descripción (solo usé lo que me contaste) y sumar lo que quieras: resultados, datos, publicación.
6. **Proyecto 5, Stakeholder for an AI End-User Support Agent**: descripción, Role y Tools.
7. **Proyecto 6, Automated Hardware Alerts for Meeting Rooms**: descripción, Role y Tools.
8. **Enlaces "Details"** de las 6 tarjetas: por ahora apuntan a `#projects`. Hay que decidir adónde van (una página por proyecto, un PDF, etc.).
9. **About me**: reescribir los dos párrafos con tus palabras.
10. **Foto**: guardar `assets/profile.jpg` y reemplazar el recuadro `photo-placeholder` por la etiqueta `<img>` que está en el comentario de esa sección.
11. **Contact**: descomentar y completar LinkedIn y GitHub (bloque marcado TODO).
12. **Versión 2** (no hecha a propósito): formulario de contacto y selector de idioma. Hay un comentario en la sección Contact que marca dónde irían.

## 5. Decisiones que tomé por mi cuenta

- **No nombré ningún empleador ni empresa.** Eso lo decidís vos más adelante.
- **No inventé resultados, métricas ni herramientas.** Todo lo que no me contaste quedó como borrador marcado.
- **Una sola página con secciones** (Projects, About me, Contact) y menú con anclas: es lo más simple de mantener y de leer en el celular.
- **Pop de color terracota** sobre crema y sage: contrasta con los verdes sin romper la calma. Se usa poco a propósito.
- **Sin JavaScript, sin librerías, sin fuentes externas:** menos cosas que se rompen, carga rápido y no depende de terceros. Las fuentes son las del sistema del visitante.
- **Idioma de la página en inglés** (`lang="en"`), porque la vas a mandar a empresas; las notas y comentarios internos están en español.
- **Texto "Electronic engineer · FIUBA"** arriba del título: salió de tus datos; cambialo si preferís otra cosa.
- **Año del footer escrito a mano (2026):** sin JavaScript no se actualiza solo; hay que cambiarlo cada enero.
- **Accesibilidad:** enlace "Skip to content", HTML semántico, enfoque visible con teclado y contraste verificado (texto principal ~12:1, secundario ~6:1; el mínimo recomendado es 4.5:1).

## 6. Cómo revisar mi trabajo

Todo está en una rama aparte llamada `diseno-v1`; `main` (lo que está publicado en anabertolino.com) no se tocó.

1. Abrí una terminal en la carpeta del proyecto y corré `git fetch` (trae la información de GitHub sin cambiar tus archivos).
2. `git checkout diseno-v1` (cambia tu carpeta a la versión nueva).
3. En VS Code, abrí la carpeta, clic derecho sobre `index.html` → **Open with Live Server**. Probá achicando la ventana para ver cómo queda en celular.
4. **Si te gusta**, para publicarla: `git checkout main`, luego `git merge diseno-v1` y `git push`. GitHub Pages la publica en unos minutos. (También podés hacer el merge desde GitHub con un Pull Request.)
5. **Si no te gusta o querés volver atrás:** `git checkout main`. Tu versión publicada sigue intacta.

## 7. Consejo: sacá el proyecto de OneDrive

Conviene mover la carpeta del proyecto **fuera de OneDrive** (por ejemplo a `C:\Proyectos\portfolio`). OneDrive sincroniza archivos en segundo plano y puede chocar con Git (archivos bloqueados, conflictos, la carpeta `.git` corrompida). Git ya es tu sistema de respaldo y versiones, así que no necesitás las dos cosas a la vez.
