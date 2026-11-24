# Prompt de la tarea programada

Crea en Claude (app de escritorio → Code → Tareas programadas) una tarea diaria a la hora del corte (p. ej. cron `0 4 * * *`) con este texto. Cambia la ruta del proyecto.

```
Trabaja en el proyecto /RUTA/A/agente-metricas-instagram.

Tarea: corte diario de las métricas de Instagram de la cuenta de config.md. Guarda UNA sola vez en la Google Sheet de config.md lo publicado entre ayer HORA_CORTE:00 y hoy HORA_CORTE:00 (zona horaria de config.md): posts, reels, carruseles e historias. No actualices filas de días anteriores: si una Clave ya está en la hoja, se salta.

Sigue al pie de la letra el skill metricas-instagram (invócalo con la herramienta Skill), pasos 0 a 8. Los pasos 7 (tablero) y 8 (WhatsApp) solo si están configurados en config.md; el 8 solo en los días de WHATSAPP_DIAS.

Herramientas: Claude in Chrome (mcp__claude-in-chrome__*) y el conector de Google Sheets.

Reglas: solo lectura en Meta. No iniciar sesión ni escribir contraseñas: si pide login, QR o verificación, detente. No inventar números. En la hoja solo añadir filas (y ordenar). Ningún mensaje de WhatsApp fuera del paso 8. Si Chrome o Sheets no están disponibles, añade "⚠️ sin métricas (motivo)" en metricas_log.md y termina. Cierra las pestañas que abras. Al terminar, añade la línea de la corrida al log y resume en español.
```

## Para que corra solo
- El computador tiene que estar encendido y despierto a esa hora, con Chrome abierto, la extensión Claude in Chrome conectada y la sesión de Meta Business Suite iniciada.
- En Mac puedes programar que se despierte unos minutos antes:

```bash
sudo pmset repeat wakeorpoweron MTWRFSU 03:55:00
```
