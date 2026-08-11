# Guia de referencia: estructura de un articulo en tu blog Hugo

Esta guia explica CADA parte del archivo `gta6-fecha-lanzamiento-confirmada.md` que te compartí:
que es, para que sirve, y que pasa visualmente si la cambias. Usala como molde
cada vez que escribas un articulo nuevo.

---

## 1. El bloque de "front matter" (los metadatos)

Es todo lo que va entre las dos lineas `+++` al inicio del archivo. Hugo lo lee
para saber COMO mostrar el articulo, pero no aparece como texto normal en la
pagina (excepto donde tu tema decida usarlo, como el titulo).

### `title`
El titulo del articulo. Aparece como encabezado principal (H1) en la pagina del
articulo, y como texto de la tarjeta en la lista de "Posts". Es tambien lo que
Google muestra en los resultados de busqueda — por eso debe tener gancho (ver
la conversacion anterior sobre titulares).

### `date`
Fecha y hora de publicacion, en formato `AAAA-MM-DDTHH:MM:SS-05:00`. Si la
fecha es futura respecto a tu reloj, Hugo OCULTA el articulo (a menos que uses
`--buildFuture`). Tambien determina el orden en que aparecen los articulos
(los mas nuevos primero).

### `draft`
`true` = borrador, no se publica nunca (ni en `hugo server` normal ni al subir
a GitHub). `false` = publicado. SIEMPRE revisa que diga `false` antes de subir
algo que quieres que se vea.

### `description`
Resumen corto (1-2 frases) usado para SEO: es el texto que Google muestra
debajo del titulo en los resultados de busqueda, y lo que se ve al compartir
el link en redes sociales (junto a la imagen de portada). No se muestra dentro
del articulo mismo.

### `summary`
Similar a `description`, pero PaperMod lo usa a veces como el texto de
"preview" debajo del titulo en las tarjetas del listado de posts (en vez de
tomar las primeras lineas del articulo automaticamente). Si lo dejas vacio,
Hugo genera un resumen automatico con las primeras palabras del cuerpo.

### `tags`
Etiquetas especificas del tema (ej. nombres de personajes, mecanicas). Sirven
para que el lector encuentre articulos relacionados por tema especifico.
Generan paginas automaticas del tipo `tusitio.com/tags/gta-6/` que listan
todos los articulos con ese tag.

### `categories`
Clasificacion mas amplia/general (ej. "Noticias", "Guias", "Teorias"). Igual
que tags, genera paginas automaticas tipo `tusitio.com/categories/noticias/`.
Diferencia practica: usa categorias para las secciones grandes de tu menu, y
tags para temas especificos dentro de esas secciones.

### El bloque `[cover]`
Controla la imagen destacada del articulo — la que aparece en la tarjeta del
listado de posts, y la que se usa cuando alguien comparte el link en redes
sociales (Facebook, Twitter, WhatsApp).

- `image`: la URL o ruta de la imagen. Puede ser una URL externa (como en el
  ejemplo) o una ruta local dentro de tu proyecto (ver seccion 4 mas abajo).
- `alt`: texto alternativo, se lee por lectores de pantalla y aparece si la
  imagen no carga. Tambien ayuda al SEO de imagenes en Google.
- `caption`: texto pequeno que aparece debajo de la imagen dentro del
  articulo (opcional, puedes dejarlo vacio quitando la linea).
- `relative`: `false` normalmente. Se pone `true` solo si usas "page bundles"
  (una carpeta por articulo con su propia imagen adentro — tema avanzado, no
  lo necesitas por ahora).
- `hidden`: `false` = se muestra. `true` = la imagen no aparece en ningun
  lado (util si solo quieres el efecto SEO sin mostrarla visualmente).

### IMPORTANTE sobre la imagen de portada de este archivo de prueba
Usé una imagen de un servicio placeholder (picsum.photos) que genera fotos
aleatorias libres de uso, SOLO para que veas el efecto visual en tu prueba
local. Antes de publicar contenido real:
- Nunca uses capturas oficiales de marketing de Rockstar sin permiso.
- Usa: capturas propias del juego (una vez publicado), fotos libres de
  derechos (Unsplash.com, Pexels.com), o graficos propios hechos en Canva.

---

## 2. El cuerpo del articulo (Markdown)

Todo lo que va DESPUES del segundo `+++` es el contenido real, escrito en
Markdown (un formato de texto simple que Hugo convierte a HTML).

| Escribes esto | Se convierte en |
|---|---|
| `## Texto` | Subtitulo grande (H2) — usa uno por seccion principal |
| `### Texto` | Subtitulo mas pequeno (H3) — para subdividir una seccion |
| `**Texto**` | **Texto en negrita** |
| `*Texto*` | *Texto en cursiva* |
| `- Texto` | Lista con vinetas |
| `[Texto](URL)` | Un link clickeable |
| `---` (linea sola) | Una linea horizontal divisoria |
| `> Texto` | Una cita destacada (blockquote) |

### ¿Por que usar `##` y no solo escribir el texto mas grande?
Porque Hugo genera automaticamente la Tabla de Contenidos (ShowToc) a partir
de estos encabezados, y Google usa esta estructura para entender de que trata
cada seccion (mejor SEO). Nunca saltes de `##` directo a `####`, mantén el
orden logico.

### La seccion de "Fuentes"
Al final del articulo de prueba veras una lista de links a los sitios de
donde saque la informacion. Esto es una buena practica de todo periodismo/
blogging serio — dale credito a tus fuentes y permite al lector verificar la
info. No es un requisito tecnico de Hugo, es una convencion que deberias
mantener en todos tus articulos con datos verificables.

---

## 3. Parametros que puedes agregar (no estan en el ejemplo, pero existen)

Estos van dentro del front matter, al mismo nivel que `title` o `tags`:

- `ShowToc = true` — fuerza mostrar la tabla de contenidos en ESTE articulo
  aunque en `hugo.toml` este desactivada globalmente (o viceversa con `false`).
- `ShowReadingTime = false` — oculta el "X min" de lectura solo en este post.
- `weight = 1` — controla el orden manual si no quieres que se ordene por
  fecha (poco usado en blogs de noticias).

---

## 4. Usar imagenes propias en vez de URLs externas

Si prefieres usar una imagen que tienes guardada en tu computadora (recomendado
para el sitio real):

1. Crea una carpeta `static/images/` dentro de tu proyecto Hugo (si no existe).
2. Copia ahi tu imagen, ej. `static/images/gta6-portada-1.jpg`.
3. En el front matter, usa: `image = 'images/gta6-portada-1.jpg'` (sin la
   palabra `static`, Hugo la agrega automaticamente al servir el sitio).

---

## 5. Como subir este articulo de prueba a tu sitio local y luego a la web

### Paso A — Colocar el archivo en tu proyecto
Descarga `gta6-fecha-lanzamiento-confirmada.md` y muevelo a:
```
C:\Users\Windows\Documents\blog-gta6\content\posts\
```

### Paso B — Verlo en local
En la terminal, dentro de la carpeta del proyecto:
```
cd C:\Users\Windows\Documents\blog-gta6
hugo server
```
Abre `http://localhost:1313/posts/` en el navegador. Deberias ver la nueva
tarjeta con imagen de portada, titulo, tiempo de lectura y descripcion.
Haz clic para entrar y revisar que los subtitulos, negritas y links se vean
bien formateados (no como texto plano).

### Paso C — Publicarlo de verdad (subir a GitHub)
Cuando estes conforme con como se ve, en la misma terminal:
```
git add .
git commit -m "Agregar articulo sobre fecha de lanzamiento de GTA 6"
git push
```
(Este `git push` ya deberia funcionar sin pedir usuario/contrasena, porque
configuramos la conexion SSH con la cuenta blogpagenotices anteriormente.)

### Paso D — Confirmar que se publico
1. Ve a `github.com/blogpagenotices/blogpagenotices.github.io/actions`
2. Espera a que el workflow mas reciente muestre el check verde ✓ (1-2 min)
3. Visita `https://blogpagenotices.github.io/posts/` y confirma que el
   articulo aparece ahi, igual que en tu localhost.

### Si algo sale mal en el Paso C o D
- Revisa que `draft = false` en el archivo.
- Revisa que la fecha no sea futura respecto al momento en que subes.
- Si el `git push` pide usuario/contrasena en vez de conectar directo,
  revisa que sigues dentro de la carpeta `blog-gta6` y que el remote siga
  usando SSH (`git remote -v` deberia mostrar una URL que empieza con
  `git@github.com-blogpagenotices`).

---

## Resumen: checklist rapido para cada articulo nuevo

- [ ] `title` con gancho, no generico
- [ ] `date` correcta (no futura) en formato `AAAA-MM-DDTHH:MM:SS-05:00`
- [ ] `draft = false` cuando este listo para publicar
- [ ] `description` y `summary` escritos (no vacios)
- [ ] Al menos 1-2 `tags` y 1 `categories`
- [ ] `[cover]` con imagen propia o libre de derechos (nunca oficial sin permiso)
- [ ] Cuerpo con `##` para cada seccion, no un solo bloque de texto
- [ ] Fuentes citadas si hay datos/afirmaciones verificables
- [ ] Revisado en `localhost:1313` antes de hacer `git push`
