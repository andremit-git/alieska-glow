# Alieska Glow · Tu tienda de maquillaje

Tu página de catálogo con carrito, lista para usar. El cliente agrega productos, y al terminar presiona **«Enviar pedido por WhatsApp»**: se abre WhatsApp con el pedido ya escrito (productos, cantidades y total) dirigido a tu número.

## Qué hay en esta carpeta

| Archivo / carpeta | Qué es |
|---|---|
| `index.html` | La tienda completa (catálogo, carrito y WhatsApp) |
| `img/` | Fotos de los productos, tu logo y los créditos de las fotos |
| `LEEME.md` | Esta guía |

Para abrirla: doble clic en `index.html` (se abre en tu navegador). Para que se vea con su tipografía bonita se necesita internet; sin internet funciona igual, solo con otra letra.

## Lo que ya quedó configurado

- **Nombre**: Alieska Glow, con tu logo (el archivo `img/logo-alieska-glow.png`). Si algún día cambias de logo, reemplaza ese archivo manteniendo el mismo nombre.
- **WhatsApp**: `+58 412-3398954`. Ya está conectado al botón de envío del pedido y a los botones «Pedidos por WhatsApp» de la página.

Si cambias de número: abre `index.html` con el Bloc de notas y busca `NUMERO_WHATSAPP`; déjalo con código de país y sin `+` ni espacios (Venezuela: `58` + celular, ej. `584123398954`). Hay un enlace `https://wa.me/584123398954` en dos lugares más (héroe y pie); cámbialos por el mismo número.

## 1. Cambia los productos

La manera fácil es el **panel de administración** (paso 5 de la sección 4): agregar, editar, poner foto y marcar disponible/agotado sin tocar código.

Si prefieres editar a mano, abre `productos.json` (o el bloque `PRODUCTOS_BASE` de `index.html`, que es el respaldo). Cada producto es una línea:

```js
{ id:1, nombre:"Labial mate «Rosa Nube»", detalle:"Cobertura total, fórmula aterciopelada", precioUsd:7, precioBs:250, disponible:true, colores:["#FF8FB1","#E02D6D"] },
```

- `nombre` y `detalle`: el texto que se muestra.
- `precioUsd` y `precioBs`: el precio en dólares y en bolívares. **Al menos uno de los dos debe estar** (`precioUsd: 7`, `precioBs: 250`, o los dos). En la tienda se muestran los dos con su moneda ($ y Bs.). Los productos antiguos que tengan solo `precio` se muestran como dólares.
- `disponible`: `true` si hay stock, `false` para marcarlo como agotado (se ve gris, dice «Agotado» y no se puede agregar).
- `colores`: los dos tonos del cuadrito de respaldo que se ve si una foto falta. Códigos de color en [htmlcolorcodes.com](https://htmlcolorcodes.com/es/).

Para agregar un producto, copia una línea y cambia el `id` por un número nuevo. Para quitar uno, borra su línea.

## 2. Fotos de los productos

Las fotos están en la carpeta `img/` con nombres `producto-1.jpg` a `producto-8.jpg` (el número es el `id` del producto). Para usar las fotos de tus propios productos: renombra tus imágenes con esos mismos nombres, reemplaza los archivos y listo — no hay que tocar el código. Si una foto falta o falla, la tarjeta muestra automáticamente el cuadro de color de respaldo.

Las fotos actuales son ejemplos de bancos de imágenes gratuitos (Flickr, Wikimedia Commons y Pexels); el autor y la licencia de cada una están en `img/CREDITOS.txt`. Si publicas la página, conserva esos créditos o reemplázalas por tus propias fotos.

## 3. Cambia los textos

Los textos del encabezado (frase principal, horarios) están escritos directamente en el HTML, por ejemplo `<h1>…</h1>`. Búscalos y edítalos con calma; no hace falta tocar nada más.

## 4. Publica la página y administra desde internet

La tienda se publica con **Netlify** (gratis) en `alieska-glow.netlify.app`, y los productos se administran desde **`/admin.html`**, un panel privado que quedó incluido. Necesitas dos cuentas gratis — **GitHub** (es el almacén donde el panel guarda tus productos) y **Netlify** (es la vitrina que publica tu tienda) — son lo único que no puedo hacer por ti.

### Paso 1 · Crea la cuenta y el repositorio

1. Entra a `github.com` y crea una cuenta gratuita.
2. Con la sesión iniciada, clic en el **+** (arriba a la derecha) → **New repository**.
3. Nombre: `alieska-glow` · Visibilidad: **Public** → **Create repository**.

### Paso 2 · Sube los archivos de esta carpeta

1. En la página del repositorio nuevo, clic en **«uploading an existing file»**.
2. Arrastra **todo lo que está dentro de esta carpeta** (index.html, admin.html, productos.json, LEEME.md y la carpeta img).
3. Clic en **Commit changes** y espera a que termine.

### Paso 3 · Publica la tienda en Netlify

1. Entra a `netlify.com` y elige **Sign up with GitHub** (usas la misma cuenta, un clic).
2. Autoriza a Netlify cuando lo pida.
3. En el panel: **Add new site → Import an existing project → Deploy with GitHub**.
4. Elige el repositorio **alieska-glow** (si no aparece, clic en «Configure the Netlify app on GitHub» y dale acceso).
5. En opciones de despliegue no cambies nada (sin build, directorio «.») → **Deploy**.
6. Espera ~1 minuto: ya tienes una dirección provisional.
7. Para que sea **alieska-glow.netlify.app**: **Site configuration → Site details → Site information → Change site name** → escribe `alieska-glow` → Save. Si el nombre está ocupado, prueba `alieska-glow-shop` u otro similar.

Tu tienda queda en: **`https://alieska-glow.netlify.app`**

A partir de aquí, cada vez que guardes cambios en el panel, Netlify publica la actualización automáticamente.

### Paso 4 · Genera tu token (la llave del panel)

1. En GitHub: clic en tu foto → **Settings** → **Developer settings** (abajo a la izquierda).
2. **Personal access tokens → Fine-grained tokens → Generate new token**.
3. En **Repository access**: «Only select repositories» → marca `alieska-glow`.
4. En **Permissions → Repository permissions → Contents**: **Read and write**.
5. Genera y copia el token (empieza por `github_pat_`).

### Paso 5 · Administra tus productos

1. Abre `tu-direccion-web/admin.html` (guárdala en favoritos).
2. Pega tu usuario, el repositorio `alieska-glow` y el token → **Conectar**.
3. Desde ahí puedes: **agregar productos** (nombre, precio en dólares y/o bolívares, descripción y foto desde tu celular), **editarlos**, **borrarlos** y activar/desactivar **disponible/agotado** con un interruptor.
4. Al terminar, presiona **«Guardar cambios en la web»**: en 1–2 minutos tu tienda pública se actualiza sola.

Seguridad: el token vive solo en el navegador donde te conectas, nunca en las páginas públicas. Usa permisos limitados a ese repositorio y revócalo cuando quieras desde GitHub. No lo compartas ni lo publiques.

## 5. Cómo llega el mensaje a tu WhatsApp

```
¡Hola! ✿ Quiero hacer un pedido:

• 1 × Labial mate «Rosa Nube» — $8,500
• 2 × Gloss «Miel Caliente» — $13,800

Total: $22,300

¿Me confirmas disponibilidad y envío? ¡Gracias!
```

El texto exacto se edita en la función `enviarWhatsApp` al final del archivo, si quieres agregar por ejemplo «Mi dirección es…».

## Siguientes pasos posibles

Cuando tengas fotos reales de todos tus productos, se pueden ajustar tamaños y encuadres. También se pueden agregar: categorías (ojos, labios, rostro), un buscador, o más productos. Solo pídemelo.
