# Configuración final de IBB Música

## 1. Activar la cuenta administradora
1. Abre https://ibb-musico.github.io/IBB-Musica/
2. En “Cuenta del equipo”, crea una cuenta con tu correo y confirma el correo si se solicita.
3. Después de registrarte, la cuenta se crea inicialmente con rol de músico. Para dar permisos de administrador hay que actualizar el rol de esa cuenta en Supabase; no se debe permitir que cualquiera se autoproclame administrador desde la página.

## 2. Autorizar la sincronización con Dropbox
La función segura `dropbox-sync` ya está desplegada en Supabase. Para que pueda leer la carpeta, necesita credenciales de una aplicación Dropbox; el vínculo del conector de ChatGPT no se puede reutilizar como token de una página web.

1. Entra en https://www.dropbox.com/developers/apps y crea una app con acceso a los archivos que autorices.
2. En la pestaña Permissions habilita `files.metadata.read` y `files.content.read`.
3. Completa el flujo OAuth de Dropbox para obtener una clave de app, secreto de app y refresh token. No publiques esos valores en GitHub ni los pegues en la página.
4. En Supabase abre https://supabase.com/dashboard/project/varubtomfyrqmidfioga/settings/functions y agrega estos secretos:
   - `DROPBOX_APP_KEY`
   - `DROPBOX_APP_SECRET`
   - `DROPBOX_REFRESH_TOKEN`
   - `DROPBOX_FOLDER_PATH` con la ruta de la carpeta que contiene las categorías (por ejemplo, `/Canciones_IBB_El_Bosque/Canciones`, si esa es la ruta exacta de tu Dropbox).
5. Guarda los secretos y vuelve a IBB Música. Inicia sesión como administrador y pulsa “Sincronizar Dropbox”.

La función comprueba el usuario administrador en Supabase, recorre la carpeta, omite títulos que ya existen e importa documentos Word. Las letras y acordes extraídos de Word requieren revisión visual antes de usarse en vivo. La sincronización es manual desde el botón; no es un proceso periódico automático.

## 3. Publicación
La web se publica gratuitamente con GitHub Pages. El dominio personalizado `ibbmusico.cl` requiere registrar/comprar el dominio y configurar sus DNS; la página de GitHub Pages sigue funcionando sin él.
