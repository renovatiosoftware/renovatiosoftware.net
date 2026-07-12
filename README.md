# Renovatio Software — sitio web (GitHub Pages)

Repo **paraguas** para el dominio **renovatiosoftware.net**. Un solo sitio sirve la landing del estudio en la raíz y cada app cuelga en su subcarpeta. Estático, sin build ni dependencias externas (CSS embebido, fuentes locales).

## Estructura

```
sitio-web/                     → raíz del repo de GitHub Pages
├── index.html                 → selector de idioma (renovatiosoftware.net/) — auto-redirige por idioma del navegador
├── en/
│   ├── index.html             → landing EN (renovatiosoftware.net/en/)
│   └── privacy/index.html     → política EN (renovatiosoftware.net/en/privacy/)
├── es/
│   ├── index.html             → landing ES (renovatiosoftware.net/es/)
│   └── privacidad/index.html  → política ES (renovatiosoftware.net/es/privacidad/)
├── CNAME                      → renovatiosoftware.net
├── robots.txt · sitemap.xml   → SEO a nivel dominio (sitemap con alternates hreflang)
├── .nojekyll
├── assets/                    → mockup + ícono ProPonte, logos Renovatio, favicon, fuentes (Onest, Geist Mono)
└── proponte/                  → app ProPonte anidada (español, estilo propio)
    ├── index.html             → renovatiosoftware.net/proponte/
    ├── politica/index.html    → renovatiosoftware.net/proponte/politica/  (Play Console / habeas data)
    ├── soporte/index.html     → renovatiosoftware.net/proponte/soporte/   (exigido por App Store)
    ├── fonts/ · logo.png · gplay.svg · .nojekyll
```

## Bilingüe (EN/ES) y SEO

La landing del estudio es bilingüe con **URLs separadas por idioma** (mejor para SEO que un toggle solo-JS):

- `/en/` y `/es/` son versiones completas; cada una declara `<link rel="alternate" hreflang>` a la otra y a `x-default` (la raíz).
- La **raíz** (`/`) es un selector: auto-redirige por `navigator.language` (ES → `/es/`, resto → `/en/`) y muestra enlaces visibles para crawlers y para quien no tenga JS.
- El **toggle EN/ES** del navbar enlaza entre las dos versiones (no traduce por JS).
- El `sitemap.xml` incluye los `xhtml:link` alternates de cada par.
- ProPonte (`/proponte/`) queda en español, independiente de este esquema.

## Publicar

Sube el contenido de esta carpeta a la **raíz** del repo de GitHub Pages. El `index.html` de la raíz queda en `renovatiosoftware.net/` y ProPonte en `renovatiosoftware.net/proponte/`. El `CNAME` (solo uno, en la raíz) fija el dominio.

## Qué se corrigió al anidar ProPonte

Se copió la web existente (`web-proponteapp`) dentro de `proponte/` y se ajustó para el dominio paraguas:

- Todas las URLs absolutas `proponteapp.com` → `renovatiosoftware.net/proponte/…` (canonical, Open Graph, Twitter, schema JSON-LD).
- Se quitó el `CNAME` propio de ProPonte (el dominio lo fija el `CNAME` de la raíz).
- El enlace del logo (`href="/"`) ahora apunta a `./` (dentro de `/proponte/`).
- El back-link de la política dejó de decir `← proponteapp.com` (dominio antiguo) y ahora es `← ProPonte`.
- Se eliminaron `robots.txt` y `sitemap.xml` internos de ProPonte (se centralizan en la raíz).
- Se **creó** la página de **soporte** (`/proponte/soporte/`), enlazada desde el menú de ProPonte.

## Notas

- **Correos por función** (crear estos alias en el dominio; EN / ES):
  - Proyectos nuevos ("Start a project" + hero): `projects@` / `proyectos@`
  - Sección de contacto: `contact@` / `contacto@`
  - Saludar / About: `hello@` / `hola@`
  - Soporte y privacidad: `support@` / `soporte@`

  ProPonte usa `soporte@renovatiosoftware.net`. El correo **renovatiossoftware@gmail.com** figura como alterno en las políticas del estudio (`/en/privacy/`, `/es/privacidad/`) y como contacto de habeas data en la política de ProPonte.
- **Logo:** el header (landing EN/ES y políticas) usa `assets/renovatio_horizontal_claro.svg` y el favicon es `assets/renovatio_icon.svg`. Las versiones oscura/vertical y el maestro editable están en `01_INSTITUCIONAL/marca/`. Hex de marca: azul `#0000FF`, amarillo `#FFFF00`, charcoal `#333333`, gris `#999999` ("Software"). El acento del sitio sigue en `#2563eb`/`#f97316` (más suave que el azul puro del logo); se puede alinear si se quiere.
- El estilo de cada app es propio: la landing del estudio es clara/premium; ProPonte conserva su estilo oscuro.
- La sección **About** presenta a Camilo Meneses (con schema.org Person + Organization) para búsquedas internacionales.
