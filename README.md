# Ownexis — sitio web

Sitio estático bilingüe (inglés / español) de Ownexis Associates, S.L., construido a
partir del dossier de capacidades. No necesita compilación ni dependencias: son
archivos HTML, CSS, JavaScript e imágenes que GitHub Pages sirve directamente.

- **Inglés:** `index.html` → `https://www.ownexis.com/`
- **Español:** `es/index.html` → `https://www.ownexis.com/es/`

---

## Publicar por primera vez

### 1. Crear el repositorio en GitHub

1. Entra en <https://github.com/new>.
2. Nombre sugerido: `ownexis-website`.
3. Visibilidad: **Public** (GitHub Pages es gratuito en repos públicos; con cuenta
   Pro también funciona en privados).
4. **No** marques «Add a README file» — este repositorio ya lo trae.
5. Pulsa **Create repository**.

### 2. Subir los archivos

**Opción A — desde el navegador (sin instalar nada):**

1. En el repositorio recién creado, pulsa **uploading an existing file**.
2. Arrastra **el contenido** de esta carpeta (no la carpeta en sí): `index.html`,
   `es/`, `assets/`, `404.html`, `CNAME`, `robots.txt`, `sitemap.xml`, etc.
3. Escribe un mensaje de commit (por ejemplo, `Publicación inicial del sitio`) y
   pulsa **Commit changes**.

> Aviso: el explorador de archivos de GitHub oculta los archivos que empiezan por
> punto. Si `.nojekyll`, `.github/` o `.gitignore` no se suben al arrastrar, usa
> la Opción B, o créalos después con **Add file › Create new file**.

**Opción B — desde la terminal (recomendada, sube todo):**

```bash
cd ownexis-website
git init
git add .
git commit -m "Publicación inicial del sitio"
git branch -M main
git remote add origin https://github.com/USUARIO/ownexis-website.git
git push -u origin main
```

Sustituye `USUARIO` por tu usuario de GitHub.

### 3. Activar GitHub Pages

1. En el repositorio: **Settings › Pages**.
2. En **Source**, elige **GitHub Actions**.

El workflow incluido (`.github/workflows/deploy.yml`) publica el sitio en cada
push a `main`. El progreso se ve en la pestaña **Actions**; el primer despliegue
tarda 1–2 minutos.

> Alternativa sin Actions: en **Source** elige *Deploy from a branch*, rama `main`
> y carpeta `/ (root)`. El archivo `.nojekyll` ya está incluido para que Pages no
> procese el sitio con Jekyll.

### 4. Conectar el dominio www.ownexis.com

El archivo `CNAME` ya contiene `www.ownexis.com`. Falta apuntar el DNS **en el
panel de tu proveedor de dominio**:

| Tipo  | Nombre | Valor                  |
|-------|--------|------------------------|
| CNAME | `www`  | `USUARIO.github.io`    |

Para que `ownexis.com` (sin `www`) redirija al sitio, añade además estos cuatro
registros `A` en el dominio raíz (`@`):

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

Después, en **Settings › Pages**, comprueba que aparece `www.ownexis.com` en
*Custom domain* y marca **Enforce HTTPS** (puede tardar unos minutos en estar
disponible mientras se emite el certificado).

**Si todavía no tienes dominio propio:** borra el archivo `CNAME` antes de subir.
El sitio quedará en `https://USUARIO.github.io/ownexis-website/`.

---

## Estructura del proyecto

```
.
├── index.html                  Página en inglés
├── es/index.html               Página en español
├── 404.html                    Página de error
├── favicon.ico
├── CNAME                       Dominio personalizado
├── robots.txt · sitemap.xml    SEO
├── .nojekyll                   Evita el procesado Jekyll de GitHub Pages
├── .github/workflows/deploy.yml
└── assets/
    ├── css/styles.css          Estilos (un único archivo)
    ├── js/main.js              Menú móvil y año del pie
    ├── docs/                   Dossieres PDF descargables
    └── img/
        ├── logo-horizontal.png        Logo para fondos claros
        ├── logo-horizontal-light.png  Logo para fondos oscuros
        ├── isotype.png / isotype-light.png
        ├── hero.jpg · founder.jpg
        ├── og-card.jpg                Imagen al compartir en redes
        ├── icon-512.png · apple-touch-icon.png
        └── projects/                  8 fotos de proyectos
```

---

## Sistema de marca

Tomado del dossier, sin cambios:

| Elemento            | Valor                                        |
|---------------------|----------------------------------------------|
| Carbón (fondo)      | `#202028`                                     |
| Oro                 | `#B89048` (oro oscuro para texto: `#9A763A`)  |
| Papel / crema       | `#FCFBF8` · `#EFECE5`                         |
| Línea               | `#D8D5CE`                                     |
| Texto secundario    | `#6B6970`                                     |
| Titulares           | Caladea (equivalente web de Cambria)          |
| Texto corrido       | Carlito (equivalente web de Calibri)          |

Caladea y Carlito son las fuentes métricamente compatibles con Cambria y Calibri,
así que la web mantiene exactamente la misma imagen que los documentos y los PPTX.
Se cargan desde Google Fonts.

Los colores viven como variables CSS al principio de `assets/css/styles.css`;
cambiar uno ahí lo cambia en todo el sitio.

---

## Cómo editar el contenido

El texto está escrito directamente en los dos HTML, sin base de datos. Para
cambiar una frase, abre `index.html` (inglés) o `es/index.html` (español), busca
el texto y edítalo. **Cualquier cambio de contenido hay que hacerlo en los dos
archivos** para que las versiones no se desincronicen.

Para ver el sitio en local antes de publicar:

```bash
cd ownexis-website
python3 -m http.server 8000
# abre http://localhost:8000
```

### Sustituir el dossier PDF

Reemplaza `assets/docs/Ownexis-Dossier-EN.pdf` y `Ownexis-Dossier-ES.pdf`
manteniendo esos nombres; los enlaces de descarga seguirán funcionando. Los PDF
actuales están protegidos contra copia, impresión y edición.

### Añadir un proyecto

1. Guarda la foto en `assets/img/projects/` (JPG, ~1000 px de ancho, bajo 250 KB).
2. Duplica un bloque `<figure>` de la sección `id="work"` en ambos idiomas y
   cambia `src`, `alt` y el pie.

---

## Pendientes recomendados

- **Foto de la sección «Nuestra misión»** (`assets/img/hero.jpg`): la que venía en
  el PPTX está en baja resolución (424 px). Conviene sustituirla por el original
  a 1600 px o más.
- **Retrato del director** (`assets/img/founder.jpg`): igual que en el dossier,
  mejorar la resolución si hay un archivo mejor.
- **Cifras del director**: verificar «30+ proyectos entregados» y «50 M€ de
  presupuesto gestionado» antes de publicar, como ya se apuntó en las notas del
  dossier.
- **Aviso legal y política de privacidad**: si el sitio va a recoger datos o
  instalar analítica, en España conviene añadir estas páginas (LSSI-CE / RGPD).
  Ahora mismo el sitio no usa cookies ni analítica, y el contacto es un `mailto:`,
  así que no hay recogida de datos.
- **Analítica** (opcional): si la quieres, usa una opción sin cookies como Plausible
  o Fathom para no tener que mostrar banner de consentimiento.

---

© Ownexis Associates, S.L. Contenido, marca e imágenes de uso exclusivo de Ownexis.
