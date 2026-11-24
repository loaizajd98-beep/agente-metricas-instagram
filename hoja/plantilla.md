# Plantilla de la Google Sheet

Crea una hoja nueva en sheets.new con estas 4 pestañas (en este orden). La fila 1 son los encabezados; no cambies el orden de las columnas.
Fechas como texto `AAAA-MM-DD HH:MM` en hora local. Las fórmulas están en formato **es_ES** (separador `;`); en `en_US` cambia `;` por `,`.

## `Publicaciones` (A:O)
Fecha publicación | Tipo | Texto | Visualizaciones | Alcance | Interacciones | Me gusta | Comentarios | Compartidos | Guardados | Seguimientos | Tiempo de reproducción | Tiempo promedio | Capturado | Clave

Tipo: `Post`, `Reel` o `Carrusel`.

## `Historias` (A:L)
Fecha y hora | Texto | Visualizaciones | Alcance | Interacciones | Me gusta | Compartidos | Respuestas | Clics en enlace | Seguimientos | Capturado | Clave

## `Resumen` (A:N)
Encabezados: Corte | Desde | Hasta | Capturado | Notas | Publicaciones | Historias | Visualizaciones publicaciones | Visualizaciones historias | Visualizaciones total | Alcance publicaciones (suma) | Alcance historias (suma) | Interacciones publicaciones | Interacciones historias

A:E los escribe el agente (una fila por corte, sin huecos). F:N son fórmulas que se ponen **solo en la fila 2** y se extienden solas:

| Celda | Fórmula |
|---|---|
| F2 | `=BYROW(B2:C;LAMBDA(v;IF(INDEX(v;1)="";"";SUMPRODUCT((Publicaciones!$A$2:$A>=INDEX(v;1))*(Publicaciones!$A$2:$A<INDEX(v;2))))))` |
| G2 | `=BYROW(B2:C;LAMBDA(v;IF(INDEX(v;1)="";"";SUMPRODUCT((Historias!$A$2:$A>=INDEX(v;1))*(Historias!$A$2:$A<INDEX(v;2))))))` |
| H2 | `=BYROW(B2:C;LAMBDA(v;IF(INDEX(v;1)="";"";SUMPRODUCT((Publicaciones!$A$2:$A>=INDEX(v;1))*(Publicaciones!$A$2:$A<INDEX(v;2))*Publicaciones!$D$2:$D))))` |
| I2 | `=BYROW(B2:C;LAMBDA(v;IF(INDEX(v;1)="";"";SUMPRODUCT((Historias!$A$2:$A>=INDEX(v;1))*(Historias!$A$2:$A<INDEX(v;2))*Historias!$C$2:$C))))` |
| J2 | `=ARRAYFORMULA(IF(B2:B="";"";H2:H+I2:I))` |
| K2 | `=BYROW(B2:C;LAMBDA(v;IF(INDEX(v;1)="";"";SUMPRODUCT((Publicaciones!$A$2:$A>=INDEX(v;1))*(Publicaciones!$A$2:$A<INDEX(v;2))*Publicaciones!$E$2:$E))))` |
| L2 | `=BYROW(B2:C;LAMBDA(v;IF(INDEX(v;1)="";"";SUMPRODUCT((Historias!$A$2:$A>=INDEX(v;1))*(Historias!$A$2:$A<INDEX(v;2))*Historias!$D$2:$D))))` |
| M2 | `=BYROW(B2:C;LAMBDA(v;IF(INDEX(v;1)="";"";SUMPRODUCT((Publicaciones!$A$2:$A>=INDEX(v;1))*(Publicaciones!$A$2:$A<INDEX(v;2))*Publicaciones!$F$2:$F))))` |
| N2 | `=BYROW(B2:C;LAMBDA(v;IF(INDEX(v;1)="";"";SUMPRODUCT((Historias!$A$2:$A>=INDEX(v;1))*(Historias!$A$2:$A<INDEX(v;2))*Historias!$E$2:$E))))` |

## `Total del día` (A1:E10)
Muestra solo el **último corte**, por tipo. Todo con fórmulas.

| Celda | Valor |
|---|---|
| A1 / B1 | `Corte` / `=INDEX(Resumen!$A:$A;MAX(FILTER(ROW(Resumen!$A$2:$A);Resumen!$A$2:$A<>"")))` |
| A2 / B2 | `Desde` / `=INDEX(Resumen!$B:$B;MAX(FILTER(ROW(Resumen!$A$2:$A);Resumen!$A$2:$A<>"")))` |
| A3 / B3 | `Hasta` / `=INDEX(Resumen!$C:$C;MAX(FILTER(ROW(Resumen!$A$2:$A);Resumen!$A$2:$A<>"")))` |
| A5:E5 | `Tipo` · `Cantidad` · `Visualizaciones` · `Alcance (suma)` · `Interacciones` |
| A6:A9 | `Post` · `Reel` · `Carrusel` · `Historia` |
| A10 | `Total del día` |

Filas 6–8 (Post, Reel, Carrusel; cambia `$A6` por `$A7`, `$A8`):
- B6 `=SUMPRODUCT((Publicaciones!$A$2:$A>=$B$2)*(Publicaciones!$A$2:$A<$B$3)*(Publicaciones!$B$2:$B=$A6))`
- C6 `=SUMPRODUCT((Publicaciones!$A$2:$A>=$B$2)*(Publicaciones!$A$2:$A<$B$3)*(Publicaciones!$B$2:$B=$A6)*Publicaciones!$D$2:$D)`
- D6 `=SUMPRODUCT((Publicaciones!$A$2:$A>=$B$2)*(Publicaciones!$A$2:$A<$B$3)*(Publicaciones!$B$2:$B=$A6)*Publicaciones!$E$2:$E)`
- E6 `=SUMPRODUCT((Publicaciones!$A$2:$A>=$B$2)*(Publicaciones!$A$2:$A<$B$3)*(Publicaciones!$B$2:$B=$A6)*Publicaciones!$F$2:$F)`

Fila 9 (Historia):
- B9 `=SUMPRODUCT((Historias!$A$2:$A>=$B$2)*(Historias!$A$2:$A<$B$3))`
- C9 `=SUMPRODUCT((Historias!$A$2:$A>=$B$2)*(Historias!$A$2:$A<$B$3)*Historias!$C$2:$C)`
- D9 `=SUMPRODUCT((Historias!$A$2:$A>=$B$2)*(Historias!$A$2:$A<$B$3)*Historias!$D$2:$D)`
- E9 `=SUMPRODUCT((Historias!$A$2:$A>=$B$2)*(Historias!$A$2:$A<$B$3)*Historias!$E$2:$E)`

Fila 10: B10 `=SUM(B6:B9)`, C10 `=SUM(C6:C9)`, D10 `=SUM(D6:D9)`, E10 `=SUM(E6:E9)`.

## Clave
`AAAA-MM-DD HH:MM Tipo primeros 20 caracteres del texto` (+ ` #n` si se repite en el mismo minuto). Sirve para no duplicar filas.
