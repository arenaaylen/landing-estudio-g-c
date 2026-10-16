# Publicar la landing desde cero

Hoy hay tres cosas enredadas: dos repos de GitHub con nombres casi iguales, un proyecto de Vercel conectado al repo equivocado, y la producción en modo "Staged" (se construye pero no se publica sola). En vez de desenredarlo, conviene borrar y rehacer.

Elegí **una** de las dos opciones. La A deja el sitio bien en 3 minutos. La B lleva 10 pero después se actualiza sola.

---

## Opción A — Sin Git, sin terminal (recomendada para salir ya)

**1. Borrar el proyecto actual de Vercel.**
vercel.com → clic en la tarjeta del proyecto `estudio-g-calafell` → pestaña **Settings** → bajar hasta el final → **Delete Project** → escribir el nombre para confirmar.

> La URL queda libre en el momento. Si al recrear te dice que el nombre está ocupado, esperá un minuto y reintentá.

**2. Descomprimir el zip.** Vas a tener una carpeta con `index.html`, `privacidad.html`, `terminos.html`, `og.png`, los íconos, `robots.txt`, `sitemap.xml`, `vercel.json` y la carpeta `api`.

**3. Subirla.**
Ir a **vercel.com/drop** → arrastrar **la carpeta entera** (o el `.zip` tal cual) a la página → en **Project Name** escribir exactamente:

```
estudio-g-calafell
```

→ **Deploy**.

**4. Verificar.** Abrí `https://estudio-g-calafell.vercel.app` con refresh forzado (`Cmd+Shift+R` o `Ctrl+F5`). Tiene que decir **"Te llaman todos los días"** en el titular.

**Para actualizar más adelante:** repetir los pasos 1 y 3 con el zip nuevo. Sí, hay que borrar y volver a subir — Drop nunca actualiza un proyecto existente.

---

## Opción B — Con GitHub, se actualiza solo

**1. Limpiar.**
- Vercel: borrar el proyecto `estudio-g-calafell` (igual que el paso 1 de la opción A).
- GitHub: borrar **los dos** repos, `estudio-g-calafell` y `estudio-gonzalez-calafell`. En cada uno: Settings → al final → Delete this repository.

> Borrar los dos es importante. Mientras existan dos nombres casi iguales, se vuelve a mezclar.

**2. Crear un repo nuevo.**
github.com → botón **+** arriba a la derecha → **New repository** → Repository name: `landing-calafell` (un nombre que no se parezca a ningún otro) → **Private** → **Create repository**.

**3. Subir los archivos.**
En el repo recién creado → **uploading an existing file** (o Add file → Upload files) → descomprimí el zip y arrastrá **todos los archivos juntos**, incluida la carpeta `api` → abajo elegí **Commit directly to the main branch** → **Commit changes**.

> `index.html` tiene que quedar en la raíz del repo, no dentro de una subcarpeta. Si arrastraste la carpeta y quedó anidado, borralo y volvé a arrastrar los archivos sueltos.

**4. Importar en Vercel.**
vercel.com → **Add New → Project** → **Import Git Repository** → elegí `landing-calafell` → en la pantalla de configuración:
- **Project Name**: `estudio-g-calafell` (exacto, así la URL queda igual)
- **Framework Preset**: Other
- Build Command y Output Directory: vacíos

→ **Deploy**.

**5. Si queda "Staged".** Abrí el deployment y, si en Environment dice *Production — Staged* en vez de *Current*, usá el menú `⋯` → **Promote to Production**. Para que no vuelva a pasar, buscá en Settings del proyecto la opción de *Rolling Releases* y desactivala.

**Para actualizar más adelante:** subís el archivo nuevo al repo (Add file → Upload files → Commit directly to main) y Vercel publica solo en menos de un minuto.

---

## Después de publicar

- [ ] El titular dice "Te llaman todos los días"
- [ ] El FAQ arranca con "¿Qué tipo de deudas trabajan?"
- [ ] Hay cuatro testimonios de Instagram
- [ ] Los botones abren WhatsApp al número +54 9 11 5657-3401
- [ ] El formulario de 3 pasos abre WhatsApp directo al tocar "Enviar mi caso"
- [ ] `/privacidad` y `/terminos` cargan sin `.html` en la URL
- [ ] Pegá el link en un chat de WhatsApp: tiene que aparecer la imagen con el titular

## Pendientes opcionales

- **Píxel de Meta**: solo si van a pautar en Instagram/Facebook. En `index.html`, reemplazar `PIXEL_ID` por el número del píxel. Si no pautan, borrar ese bloque.
- **Guardar los leads**: en Vercel → Settings → Environment Variables, agregar `LEAD_WEBHOOK_URL` con una URL de Zapier, Make o un Google Apps Script. Sin eso, la consulta solo llega por WhatsApp.
