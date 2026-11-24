# Agente de métricas de Instagram → Google Sheets

Un skill para **Claude Code** que cada día, a una hora fija, toma las métricas de una cuenta de Instagram (posts, reels, carruseles e historias) desde **Meta Business Suite** y las guarda en una **Google Sheet**. Opcionalmente pasa el total del día a un tablero web y, los fines de semana, envía una captura a un grupo de **WhatsApp**.

Todo corre en tu computador con **Claude in Chrome** (tu propia sesión del navegador): no usa la API de Instagram, no necesita apps de Meta ni tokens, y no cuesta créditos extra.

## Qué hace
1. **Corte diario a hora fija** (por defecto 4 am): guarda **una sola vez** lo publicado entre ayer 04:00 y hoy 04:00. Nunca reescribe días anteriores.
2. **Hoja de cálculo:** añade una fila por publicación y por historia. Los totales del día (por tipo y en total) los calculan **fórmulas de la hoja**, no los totales de Meta.
3. **Recupera días perdidos:** si el computador estuvo apagado, procesa los cortes que falten (hasta 7 días).
4. **Tablero (opcional):** escribe el total de visualizaciones del día en una casilla por día de un tablero web.
5. **WhatsApp (opcional):** sábados y domingos envía una captura del tablero a un grupo, como foto.

## Requisitos
- [Claude Code](https://claude.com/claude-code) en la app de escritorio (para tareas programadas).
- Extensión **Claude in Chrome** conectada, con la sesión de Meta Business Suite iniciada en ese Chrome.
- Conector de **Google Sheets** en Claude.
- Para el paso 8: WhatsApp Web vinculado en ese mismo Chrome.
- El computador encendido a la hora del corte.

## Instalación
1. Clona el repositorio y ábrelo en Claude Code.
2. Copia `config.example.md` como `config.md` y llena tus datos (cuenta, `asset_id`, ID de la hoja y, si los usas, tablero y grupo).
3. Crea la Google Sheet con las pestañas y fórmulas de [`hoja/plantilla.md`](hoja/plantilla.md).
4. Prueba a mano: pide en Claude Code "saca las métricas".
5. Crea la tarea programada con el texto de [`tarea-programada.md`](tarea-programada.md).

## Estructura
```
.claude/skills/metricas-instagram/
  SKILL.md            # el flujo completo, paso a paso
  scripts/extraer.js  # lee la tabla de Business Suite (solo lectura)
config.example.md     # plantilla de configuración (config.md no se sube)
hoja/plantilla.md     # pestañas, columnas y fórmulas de la hoja
tarea-programada.md   # prompt de la tarea diaria
```

## Lo que aprendimos de Business Suite y WhatsApp Web
- Abre siempre Business Suite con `?asset_id=...`: sin él puede abrir otra cuenta del mismo usuario.
- Activa **Filtrar → Ubicación → Feed de Instagram** en cada corrida: sin él, las publicaciones cruzadas traen números de Facebook. El filtro no queda en la URL.
- La tabla solo carga más filas con la **rueda del ratón**; el scroll por JavaScript no funciona.
- `javascript_tool` corta la salida en ~1000 caracteres: el extractor deja el JSON en un `<article>` y se lee con `get_page_text`.
- En WhatsApp Web, el único campo de archivo del menú Adjuntar es el de **stickers**: la imagen se envía **pegándola** en el chat (ver el paso 8 del skill).

## Seguridad
- Solo lectura en Meta: el agente no publica, edita, borra, promociona ni exporta.
- No escribe contraseñas ni inicia sesión: si algo pide login, QR o verificación, se detiene.
- En la hoja solo añade filas; nunca modifica ni borra las existentes.
- El único mensaje que envía es la captura del paso 8, al grupo configurado y en los días configurados.
- Automatizar WhatsApp Web puede ir contra sus condiciones de uso: úsalo con moderación y bajo tu responsabilidad.

## Limitaciones
- Depende de la interfaz de Business Suite y WhatsApp Web: si Meta cambia la página, puede que haya que ajustar el skill o el extractor.
- El computador tiene que estar encendido; si no, la siguiente corrida recupera los días faltantes, pero con números más nuevos.
- Business Suite no siempre lista todas las historias, sobre todo las de más de un día.
