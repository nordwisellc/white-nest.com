# White Nest Management — sitio web

Sitio estático (HTML + CSS + un poco de JS). Sin frameworks, sin compilación: lo que hay en el
repositorio es exactamente lo que se publica.

```
index.html          Inicio
servicios.html      Planes (Online / Integral / Premium) + Set Up
asesoramiento.html  Consultoría
about.html          Nuestro objetivo, historia y equipo
contacto.html       Formulario de contacto
terminos.html       Términos y condiciones (plantilla, revisar)
privacidad.html     Política de privacidad (plantilla, revisar)
404.html            Página de error
CNAME               Dominio personalizado
assets/css/style.css
assets/js/main.js
assets/img/         Imágenes
```

---

## 1. Sustituir las imágenes

En `assets/img/` hay un marcador de posición por cada foto, con el nombre ya puesto.
**Sustituye el archivo manteniendo exactamente el mismo nombre** y la web se actualiza sola.

| Archivo | Dónde aparece |
|---|---|
| `hero-salon.jpg` | Fondo del hero de Inicio |
| `llaves-madera.jpg` | Sección "Expertos en gestión" |
| `salon-verde.jpg` | Testimonio de María López (Inicio) |
| `sofa-oscuro.jpg` | Banda de testimonios (todas las páginas) |
| `sofa-salon.jpg` | Hero de Asesoramiento |
| `planta-salon.jpg` | "Nuestro Objetivo" (About) y fondo de Contacto |
| `escritorio-portatil.jpg` | Sección de consultoría (Asesoramiento) |
| `plan-online.jpg` / `plan-integral.jpg` / `plan-premium.jpg` | Cabecera de cada plan |
| `setup-basico.jpg` / `setup-premium.jpg` | Bloques de Set Up |
| `equipo-hugo.jpg` / `equipo-patricia.jpg` | Fotos del equipo (cuadradas) |
| `testimonio-maria.jpg` / `-andres.jpg` / `-sofia.jpg` | Avatares de los testimonios (cuadradas) |
| `viaje-01.jpg` … `viaje-16.jpg` | Las dos rejillas de fotos de About (cuadradas) |
| `logo-airbnb.png` / `logo-booking.png` / `logo-vrbo.png` | Logos de plataformas en Inicio |

Consejos rápidos:

- Las de fondo (hero, sofá, planta) mejor **horizontales y ≥ 1600 px de ancho**.
- Las de equipo, testimonios y viajes, **cuadradas**.
- Los tres logos de plataformas, **PNG con fondo transparente**, descargados de las páginas
  oficiales de prensa/partners de cada plataforma (Airbnb, Booking.com y Vrbo tienen su propio
  kit de marca y sus condiciones de uso).
- Comprime las fotos antes de subirlas (squoosh.app o tinypng.com). Objetivo: menos de 300 KB
  por imagen.

El logotipo (`logo-white-nest.svg`) y el favicon (`favicon.svg`) son vectoriales y redibujados a
partir de las capturas. Si tienes el archivo original del logo, sustitúyelo también.

---

## 2. Subirlo a GitHub

Desde la carpeta del proyecto:

```bash
git init
git add .
git commit -m "Web de White Nest Management"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/white-nest.git
git push -u origin main
```

---

## 3. Publicar en GitHub Pages

1. En el repositorio: **Settings → Pages**.
2. En *Build and deployment* → *Source*, elige **GitHub Actions**.
   (El workflow `.github/workflows/deploy.yml` ya está incluido y publica en cada `push` a `main`.)
3. Espera a que el Action termine en verde. La web ya está online en
   `https://TU_USUARIO.github.io/white-nest/`.

---

## 4. Conectar el dominio

El archivo `CNAME` está configurado con `www.white-nest.com`. **Si tu dominio es otro, edítalo**
(una sola línea, sin `https://` y sin barra final) antes de configurar el DNS.

### En el panel de tu proveedor de dominio

Crea estos registros:

| Tipo | Nombre / Host | Valor |
|---|---|---|
| CNAME | `www` | `TU_USUARIO.github.io` |
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |

Los cuatro registros A hacen que `white-nest.com` (sin www) redirija al dominio con www.

### En GitHub

1. **Settings → Pages → Custom domain**: escribe `www.white-nest.com` y guarda.
2. Espera a que aparezca el check verde de verificación del DNS (puede tardar de unos minutos a
   24 horas).
3. Marca **Enforce HTTPS**. GitHub emite el certificado automáticamente.

---

## 5. Cambios habituales

- **Teléfonos, email y redes sociales**: están en el `<footer>` de cada página HTML. Los enlaces
  de Facebook, Instagram y TikTok apuntan de momento a la portada de cada red — cámbialos por
  las URLs reales de los perfiles de White Nest.
- **Colores**: todos definidos como variables al principio de `assets/css/style.css`
  (`--cream: #f7ede2`, `--blush: #d4c0b5`, `--brown: #857160`, `--ink: #121826`).
- **Tipografía**: Outfit, cargada desde Google Fonts en el `<head>` de cada página.
- **Formulario de contacto**: ahora abre el gestor de correo del visitante
  (`mailto:info@white-nest.com`). Para recibir los envíos directamente en la bandeja sin que se
  abra el cliente de correo, crea una cuenta gratuita en [Formspree](https://formspree.io) y en
  `contacto.html` cambia la etiqueta del formulario por:
  ```html
  <form class="form-card" action="https://formspree.io/f/TU_ID" method="POST">
  ```
  (quitando el atributo `enctype`). Hay un comentario en el propio archivo recordándolo.
- **Textos legales**: `terminos.html` y `privacidad.html` son plantillas de partida. Revísalas
  con tu asesor y completa los datos identificativos antes de publicar.
