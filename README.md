# ownexis.com — sitio web

Sitio estático (HTML + CSS + JS, sin dependencias ni proceso de compilación) listo para publicar en **GitHub Pages** con el dominio **www.ownexis.com** registrado en **GoDaddy**.

Contenido y fotografía tomados del dosier de capacidades **Ownexis-Dossier-4-Sectores-REV**: cuatro sectores — Hotelero, F&B, Terciario y Residencial.

---

## 1. Estructura

```
/
├── index.html              Página principal (inglés)
├── legal.html              Aviso legal y privacidad (inglés)
├── 404.html                Página de error
├── es/
│   ├── index.html          Página principal (español)
│   └── legal.html          Aviso legal y privacidad (español)
├── assets/
│   ├── css/styles.css      Sistema de diseño Ownexis + capa web
│   ├── js/main.js          Menú móvil, animaciones, formulario y ventana de gracias
│   └── img/
│       ├── ownexis-logo-light.png / -color.png / -dark.png
│       ├── ownexis-isotype-light.png / -color.png / -dark.png
│       ├── og-image.jpg                Vista previa en WhatsApp / LinkedIn
│       ├── favicon-32.png, apple-touch-icon.png, icon-192.png, icon-512.png
│       └── photos/                     Fotografía del dosier (ver README de la carpeta)
├── favicon.ico
├── CNAME                   Contiene: www.ownexis.com
├── .nojekyll               Evita el procesado Jekyll de GitHub Pages
├── robots.txt · sitemap.xml · site.webmanifest
```

Secciones de la página: portada · la propuesta · cuatro sectores · servicios principales · metodología · la diferencia Ownexis · gobernanza · experiencia del fundador · trayectoria · referencias · modalidades de contratación · formulario de contacto.

---

## 2. Formulario de contacto — IMPORTANTE

GitHub Pages solo sirve archivos estáticos: **no puede enviar correo por sí mismo**. El formulario necesita un servicio externo que reciba el mensaje y lo reenvíe a info@ownexis.com.

**Estado actual:** sin servicio configurado, al pulsar *Enviar* se abre el cliente de correo del visitante con el mensaje ya redactado y aparece igualmente la ventana de agradecimiento. Funciona, pero depende de que el visitante tenga correo configurado en su dispositivo.

**Configuración recomendada (5 minutos, gratuita):**

1. Crear una cuenta en [formspree.io](https://formspree.io) y un formulario nuevo con destino `info@ownexis.com`.
2. Copiar la URL que genera, del tipo `https://formspree.io/f/abcdwxyz`.
3. Abrir `assets/js/main.js` y pegarla en la primera línea de configuración:

```js
var FORM_ENDPOINT = "https://formspree.io/f/abcdwxyz";
```

4. Guardar y subir el cambio. A partir de ahí los mensajes llegan al correo directamente y la ventana de agradecimiento aparece al confirmarse el envío.

Alternativas equivalentes: [web3forms.com](https://web3forms.com), [getform.io](https://getform.io). Cualquiera que acepte un `POST` en JSON funciona sin tocar nada más.

El formulario incluye un campo trampa oculto (*honeypot*) contra bots y validación de nombre, correo y nota antes del envío.

---

## 3. Antes de publicar — 2 datos por completar

1. **`legal.html` y `es/legal.html`**: sustituir `[B-XXXXXXXX]`, el domicilio social, los datos del Registro Mercantil y `[ciudad]` por los datos reales de Ownexis, S.L.
2. **Logo en versión clara**: `ownexis-logo-light.png` e `ownexis-isotype-light.png` proceden del dosier. Cuando el diseñador entregue los archivos oficiales, sobrescribir esos dos ficheros con el mismo nombre.

Opcional: reemplazar las fotos de baja resolución indicadas en `assets/img/photos/README.md`.

---

## 4. Publicar en GitHub Pages

### 4.1 Crear el repositorio

1. GitHub → **New repository**. Nombre: `ownexis-web`. Visibilidad: **Public** (Pages gratuito lo exige).
2. No añadir README ni .gitignore.

### 4.2 Subir los archivos

**Opción A — sin línea de comandos:** en el repositorio vacío, *uploading an existing file*, y arrastrar **el contenido** de esta carpeta (no la carpeta en sí: `index.html` debe quedar en la raíz del repositorio).

**Opción B — con Git:**

```bash
cd ownexis-site
git init
git add .
git commit -m "Ownexis website — initial release"
git branch -M main
git remote add origin https://github.com/USUARIO/ownexis-web.git
git push -u origin main
```

Comprobar que `CNAME` y `.nojekyll` se han subido: son archivos sin extensión o que empiezan por punto y algunos exploradores los ocultan.

### 4.3 Activar Pages

1. Repositorio → **Settings** → **Pages**.
2. *Source*: **Deploy from a branch**. *Branch*: `main`, carpeta `/ (root)`. **Save**.
3. En *Custom domain* escribir `www.ownexis.com` y **Save**.
4. Marcar **Enforce HTTPS** en cuanto GitHub lo habilite (aparece tras validar el DNS).

---

## 5. DNS en GoDaddy

GoDaddy → **Mis productos** → `ownexis.com` → **DNS** → **Administrar zonas DNS**.

**Registro para www:**

| Tipo  | Nombre | Valor               | TTL    |
|-------|--------|---------------------|--------|
| CNAME | `www`  | `USUARIO.github.io` | 1 hora |

Sustituir `USUARIO` por el usuario u organización de GitHub. No incluir el nombre del repositorio.

**Registros para el dominio raíz** (cuatro registros A, nombre `@`):

| Tipo | Nombre | Valor             | TTL    |
|------|--------|-------------------|--------|
| A    | `@`    | `185.199.108.153` | 1 hora |
| A    | `@`    | `185.199.109.153` | 1 hora |
| A    | `@`    | `185.199.110.153` | 1 hora |
| A    | `@`    | `185.199.111.153` | 1 hora |

Opcionalmente los AAAA equivalentes: `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`.

**Limpieza:** eliminar el registro A `@` de la página aparcada de GoDaddy y el CNAME `www` → `@` si existe. **No tocar los registros MX ni TXT**: si el correo `info@ownexis.com` se gestiona desde GoDaddy o Microsoft 365, borrarlos deja el correo sin servicio.

**Verificación:**

```bash
dig www.ownexis.com +short      # USUARIO.github.io y una IP 185.199.x.x
dig ownexis.com +short          # las cuatro IP 185.199.x.x
```

La propagación tarda entre 10 minutos y 48 horas, habitualmente menos de una hora.

---

## 6. Notas técnicas

- Sin frameworks ni compilación: la misma carpeta sirve en Netlify, Cloudflare Pages o cualquier hosting estático.
- Tipografías desde Google Fonts (Gelasio ≈ Cambria, Carlito ≈ Calibri). Para eliminar esa dependencia externa —y con ella la mención de terceros del aviso legal— basta descargar los `.woff2` a `assets/fonts/` y sustituir el `<link>` por reglas `@font-face`.
- Responsive, imprimible, navegable por teclado y sin cookies propias.
- Bilingüe con `hreflang`: inglés en la raíz, español en `/es/`. Al editar textos hay que actualizar ambas versiones.
- Los contenidos proceden del dosier de capacidades; mantener la coherencia con él, en especial las cláusulas de independencia, separación OR/PM y honorarios.
