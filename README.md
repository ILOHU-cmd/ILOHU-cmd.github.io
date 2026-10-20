# Portafolio — Emerson Ballesteros Díaz

Sitio estático de portafolio profesional construido con [Quarto](https://quarto.org) y publicado con GitHub Pages desde la rama `main`, carpeta `docs/`.

**Objetivo:** presentar mi perfil como estudiante de Ingeniería en Ciencia de Datos (UIS) y conseguir mi primera oportunidad como **Data Analyst** o **Security Data Analyst**, con proyección hacia el **Blue Team**.

## Stack

- **Quarto** (sitio web estático)
- Tema **cosmo** + `custom.scss`
- **GitHub Pages** (rama `main`, carpeta `/docs`)
- Python para los proyectos de análisis

## Estructura del repositorio

```text
.
├── _quarto.yml                  # Configuración del sitio
├── custom.scss                  # Estilos propios
├── index.qmd                    # Sobre mí
├── projects.qmd                 # Listado de proyectos
├── cv.qmd                       # CV y certificados
├── contact.qmd                  # Contacto
├── projects/
│   ├── _template.qmd            # Plantilla (Quarto ignora archivos con "_")
│   ├── deteccion-anomalias-logs.qmd
│   ├── polla-familiar.qmd
│   └── electrolineras-uis.qmd
├── assets/                      # CV en PDF e imágenes
├── docs/                        # Salida generada por Quarto (GitHub Pages)
├── requirements.txt             # Dependencias Python de los proyectos
├── .gitignore
└── README.md
```

> `docs/` es generado por Quarto. No edites esos archivos a mano: se sobrescriben en cada render.

## Requisitos

- Quarto 1.10 o superior
- Python 3.11 o superior (solo si vas a ejecutar los notebooks de los proyectos)
- Git

## Instalación de Quarto en Debian

### Opción A — instalación local, sin `sudo` (recomendada)

```bash
mkdir -p ~/.local/opt ~/.local/bin

wget -O /tmp/quarto.tar.gz \
  https://github.com/quarto-dev/quarto-cli/releases/download/v1.10.19/quarto-1.10.19-linux-amd64.tar.gz

tar -xzf /tmp/quarto.tar.gz -C ~/.local/opt
ln -sfn ~/.local/opt/quarto-1.10.19 ~/.local/opt/quarto
ln -sf ~/.local/opt/quarto/bin/quarto ~/.local/bin/quarto

quarto --version
```

Si `~/.local/bin` no está en el `PATH`, agrégalo al final de `~/.bashrc`:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

### Opción B — instalación para todo el sistema (requiere `sudo`)

```bash
wget https://github.com/quarto-dev/quarto-cli/releases/download/v1.10.19/quarto-1.10.19-linux-amd64.deb
sudo dpkg -i quarto-1.10.19-linux-amd64.deb
quarto --version
```

Quarto incluye Pandoc y Deno; no hace falta instalarlos por separado.

## Uso local

```bash
# Vista previa con recarga automática
quarto preview

# Generar el sitio en docs/
quarto render
```

Para el entorno de Python de los proyectos:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Publicación en GitHub Pages

1. Haz commit y push de `docs/` a `main`.
2. En GitHub, entra a **Settings → Pages**.
3. En **Build and deployment**, elige **Deploy from a branch**.
4. Selecciona la rama **main** y la carpeta **/docs**. Guarda.
5. El sitio queda en `https://ilohu-cmd.github.io/`.

`docs/.nojekyll` evita que GitHub Pages procese el sitio con Jekyll.

Flujo típico después de editar contenido:

```bash
quarto render
git add .
git commit -m "docs: actualiza el sitio"
git push origin main
```

## Cómo agregar un proyecto

```bash
cp projects/_template.qmd projects/mi-nuevo-proyecto.qmd
```

1. Cambia el título, la descripción, la fecha y las categorías del front matter.
2. Completa las seis secciones: **Problema, Datos, Método, Resultados, Insight de negocio, Enlace al repo**.
3. Reemplaza todos los `[COMPLETAR]` por información real.
4. Agrega una tarjeta en `projects.qmd`.
5. Ejecuta `quarto render` y revisa la página.

## Pendientes antes de publicar

- [ ] Reemplazar el correo y el enlace de LinkedIn en `contact.qmd`, `cv.qmd` e `index.qmd`.
- [ ] Agregar el PDF del CV en `assets/emerson-ballesteros-cv.pdf` (ahora hay un marcador de posición).
- [ ] Completar fechas y enlaces de verificación de los certificados de Google.
- [ ] Completar las métricas reales de cada proyecto.
- [ ] Publicar el repositorio del proyecto de detección de anomalías y enlazarlo.
- [ ] Agregar una demo de Polla Familiar (por ejemplo, Streamlit Community Cloud).
- [ ] Revisar que no haya datos personales, credenciales ni tokens en el sitio.
- [ ] Configurar GitHub Pages con `main` y `/docs`.

## Notas

- Los archivos que empiezan con `_` (como `projects/_template.qmd`) no se renderizan; sirven como plantilla.
- Los enlaces a `.qmd` se convierten automáticamente en enlaces `.html` al generar el sitio.
- Si agregas notebooks con salidas pesadas, considera `execute: freeze: auto` en `_quarto.yml` y versionar `_freeze/`.
- El contenido y el código de este repositorio son de Emerson Ballesteros Díaz.
