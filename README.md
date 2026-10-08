# Ojo de Director — guía de publicación

App web instalable (PWA) que critica piezas de diseño gráfico con IA.
Sube o fotografía una pieza y recibe una crítica de director de arte.

## Qué contiene
- `public/` — la app (pantalla, ícono, instalación en el teléfono).
- `api/critica.js` — el servidor que habla con la IA (guarda tus claves).
- `api/_prompt.js` — el prompt y la base de conocimiento de diseño. Aquí editas los criterios.
- `.env.example` — lista de ajustes.

## Paso 1. Consigue la clave gratis de NVIDIA
1. Entra a https://build.nvidia.com e inicia sesión (te pedirá unirte al programa de desarrolladores, que es gratis).
2. Ve a https://build.nvidia.com/settings/api-keys y pulsa **Generate Key**.
3. Copia la clave (empieza por `nvapi-`).

## Paso 2. Publica en Vercel (gratis)
1. Crea una cuenta en https://vercel.com (puedes entrar con GitHub).
2. Sube esta carpeta a un repositorio de GitHub y en Vercel pulsa **Add New → Project → Import**.
   (Alternativa: instala el CLI con `npm i -g vercel` y ejecuta `vercel` dentro de esta carpeta.)
3. En **Settings → Environment Variables** añade:
   - `PROVIDER` = `nvidia`
   - `NVIDIA_API_KEY` = tu clave `nvapi-...`
   - `APP_PASSWORD` = una clave larga que inventes (solo quien la tenga podrá usar la app)
4. Pulsa **Deploy**. Vercel te dará una dirección tipo `https://tu-app.vercel.app`.

## Paso 3. Instálala en el teléfono
Abre la dirección en Chrome (Android) o Safari (iPhone) y elige **Instalar aplicación** o **Añadir a pantalla de inicio**.
La primera vez que critiques, la app te pedirá la `APP_PASSWORD`.

## Cambiar a Claude (mejor calidad)
En Vercel cambia `PROVIDER` a `claude` y añade `ANTHROPIC_API_KEY` (de https://console.anthropic.com). Cada crítica tiene un costo pequeño.
Vuelve a desplegar (Deployments → Redeploy) para aplicar los cambios.

## Si algo falla
- **"Falta NVIDIA_API_KEY"**: no guardaste la variable o no redesplegaste.
- **Error de formato de imagen con NVIDIA**: pon `NVIDIA_IMAGE_FORMAT` = `tag`, o prueba otro modelo de visión del catálogo en `NVIDIA_MODEL`.
- **Límite del plan gratuito**: NVIDIA permite unas 40 peticiones por minuto por modelo; espera un minuto.
- **Calidad de la crítica baja**: los modelos gratuitos son menos precisos que Claude; prueba otro modelo o cambia a `claude`.
- El plan gratuito de NVIDIA es para desarrollo y pruebas; si lanzas la app al público, revisa sus términos.

## Seguridad
Nunca pongas las claves dentro de `public/`. Solo van en las variables de entorno de Vercel.
