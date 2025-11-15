# Ì∫Ä Desplegar en Render

## Paso 1: Preparar el repositorio
‚úÖ Ya lo tienes hecho (este fork)

## Paso 2: Crear Web Service en Render

1. Ve a [https://dashboard.render.com/](https://dashboard.render.com/)
2. Click en **"New +"** ‚Üí **"Web Service"**
3. Conecta tu repositorio de GitHub: `https://github.com/PedroPVergara/MyM3U.git`
4. Configura:
   - **Name**: `stremio-iptv-addon` (o el nombre que quieras)
   - **Runtime**: `Node`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Instance Type**: `Free` (para empezar)

## Paso 3: Variables de entorno en Render

En la secci√≥n **Environment**, agrega estas variables:

```
CACHE_ENABLED=true
CACHE_TTL_MS=21600000
MAX_CACHE_ENTRIES=300
PREFETCH_ENABLED=true
PREFETCH_MAX_BYTES=5000000
DEBUG_MODE=false
NODE_ENV=production
```

### Ì¥ê IMPORTANTE - Seguridad (MUY RECOMENDADO):

Para evitar que cualquiera pueda ver tus credenciales en el token, agrega:

```
CONFIG_SECRET=GENERA_UN_SECRETO_ALEATORIO_MUY_LARGO_MINIMO_32_CARACTERES
```

**C√≥mo generar un secreto seguro:**
```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

## Paso 4: Deploy

Click en **"Create Web Service"** y espera 2-5 minutos.

Tu addon estar√° en: `https://tu-nombre.onrender.com/`

## Paso 5: Mantenerlo activo (UptimeRobot)

Render FREE duerme las apps sin tr√°fico. Para evitarlo:

1. Ve a [https://uptimerobot.com/](https://uptimerobot.com/) (gratis)
2. Crea una cuenta
3. Add New Monitor:
   - **Monitor Type**: HTTP(s)
   - **Friendly Name**: Stremio IPTV Addon
   - **URL**: `https://tu-nombre.onrender.com/health`
   - **Monitoring Interval**: 5 minutes
4. Save ‚Üí ¬°Listo! Tu servicio estar√° siempre activo

## Ì≥ù Uso despu√©s del deploy

1. Abre `https://tu-nombre.onrender.com/`
2. Configura tu playlist M3U o Xtream Codes
3. Copia el manifest URL que aparece
4. Agr√©galo en Stremio como addon

## ‚ö†Ô∏è Notas importantes

- El plan FREE de Render tiene l√≠mites de CPU/mes
- Si usas mucho, considera upgrade a plan de pago ($7/mes)
- Nunca compartas tu token p√∫blico si tiene credenciales sensibles
- Usa CONFIG_SECRET para encriptar tokens
