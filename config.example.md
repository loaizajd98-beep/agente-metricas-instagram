# Configuración del agente de métricas

Copia este archivo como `config.md` y llena tus datos. `config.md` está en `.gitignore`: no lo subas.

## Instagram / Meta Business Suite
- CUENTA: `tu_usuario_de_instagram` (sin @; el agente comprueba que la tabla muestre esta cuenta)
- ASSET_ID: `000000000000000` (número que aparece en la URL de Business Suite como `asset_id=...` al abrir tu cuenta)
- ZONA_HORARIA: `America/Mexico_City` (la tuya, formato IANA)
- HORA_CORTE: `4` (hora local del corte diario; cámbiala también en `scripts/extraer.js`)

## Google Sheet
- SHEET_ID: `ID_DE_TU_HOJA` (lo que va entre `/d/` y `/edit` en la URL)
- sheetId de pestañas (para ordenar): Publicaciones = `0`, Historias = `1`
- Configuración regional de la hoja: `es_ES` (fórmulas con `;`) o `en_US` (fórmulas con `,`)

## Paso 7 · Tablero web (opcional; borra estas líneas si no lo usas)
- TABLERO_URL: `https://...`
- TABLERO_SECCION: `Vistas` (pestaña o sección donde está la fila de vistas por día)

## Paso 8 · WhatsApp (opcional; borra estas líneas si no lo usas)
- WHATSAPP_GRUPO: `Nombre exacto del grupo`
- WHATSAPP_BUSQUEDA: `texto para buscarlo`
- WHATSAPP_DIAS: `sábado, domingo`
- WHATSAPP_TEXTO: `` (vacío = solo la imagen)
