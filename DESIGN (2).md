# DESIGN.md — Reservas USFQ

Sistema de diseño y guía de estilo del frontend. Léelo antes de crear o modificar cualquier pantalla o componente. Si una spec contradice este archivo, manda la spec y hay que actualizar este archivo en el mismo commit. Todo lo de aquí está también en `docs/diseno/brand-board.html`: si una decisión está en uno, debe estar en el otro. Las reglas de negocio viven en `docs/prd/prd.md`.

## Concepto

Reservar un equipo o un espacio debe sentirse como pedir algo en una tienda en línea: claro, rápido y sin sorpresas.

**Nombre de trabajo:** Reservas USFQ (provisional, el equipo puede cambiarlo).
**Palabras clave:** claro · rápido · confiable.
**Dirección visual:** moderna y funcional, dentro de la marca USFQ: rojo, negro y blanco, mucho espacio en blanco y un solo color de acción.

## Usuarios y contexto de uso

- **Estudiantes y profesores:** reservan desde el celular entre clases, de pie, con poco tiempo. Necesitan elegir fecha, ver qué hay libre y enviar la solicitud en pocos pasos. Responsive es prioridad.
- **Administradores (Santiago y Luis Daniel):** trabajan en una computadora, en el mostrador, con filas de gente. Necesitan ver las solicitudes en revisión, aprobar o rechazar y corregir carritos con pocos clics.
- **Idioma:** toda la interfaz existe en español (por defecto) e inglés. Ningún texto va escrito dentro de una imagen.
- **Horario:** retiros y devoluciones de lunes a viernes, 8:00–17:20, hora de Quito.

## Principios

1. **La fecha primero:** antes de ver productos, el usuario elige cuándo los necesita.
2. **Un solo botón primario por pantalla,** en rojo.
3. **Cada estado tiene su mensaje y su icono:** nunca se comunica solo con color.
4. **Cada error dice qué pasó y cómo arreglarlo,** sin culpar al usuario.
5. **Menos pasos:** si algo puede asumirse (fecha ya elegida, nota opcional), no se pregunta.

## Color

Usa solo estas variables. No escribas colores directamente en los componentes. El rojo y el negro vienen del manual de identidad USFQ 2024; el resto es del sistema.

| Variable | Valor | Nombre | Uso |
|---|---|---|---|
| `--color-primario` | `#E11B22` | Rojo USFQ | Botón primario, barra superior, selección activa |
| `--color-primario-hover` | `#B3151B` | Rojo oscuro | Estado hover y presionado del botón primario |
| `--color-enlace` | `#C41B1E` | Rojo enlace | Enlaces y texto rojo sobre blanco o gris claro |
| `--color-texto` | `#231F20` | Negro USFQ | Texto principal, botón oscuro |
| `--color-texto-secundario` | `#5C5F62` | Gris tinta | Ayudas, fechas, etiquetas menores |
| `--color-fondo` | `#F5F5F5` | Gris claro | Fondo de página |
| `--color-superficie` | `#FFFFFF` | Blanco | Tarjetas, formularios, modales |
| `--color-borde` | `#D9DADB` | Borde | Bordes decorativos y separadores |
| `--color-borde-campo` | `#767779` | Borde de campo | Borde de campos y casillas (4,5:1) |
| `--color-foco` | `#1D4F91` | Azul foco | Anillo de foco del teclado (3 px) |

### Colores de estado

El texto va siempre sobre su propio fondo; todas las combinaciones superan 4,5:1. Cada estado lleva además icono y texto.

| Variable (texto / fondo) | Valor | Usos |
|---|---|---|
| `--estado-ok` / `--estado-ok-fondo` | `#1B6B3A` / `#E3F3E8` | Disponible, Aprobada, éxito |
| `--estado-aviso` / `--estado-aviso-fondo` | `#7A4A00` / `#FBF1DF` | En revisión, Mantenimiento, avisos |
| `--estado-error` / `--estado-error-fondo` | `#B3261E` / `#FBECEA` | Rechazada, Dañado, errores |
| `--estado-info` / `--estado-info-fondo` | `#1D4F91` / `#E6EEF8` | Retirada (en curso) |
| `--estado-neutro` / `--estado-neutro-fondo` | `#3F4245` / `#ECEDEE` | Devuelta, Cancelada, Vencida, No disponible, Extraviado |

Reglas de uso:
- El rojo `#E11B22` solo es texto sobre blanco; sobre gris claro o negro usa `--color-enlace` o blanco, porque no llega a 4,5:1.
- No uses rojo de marca para errores: los errores usan `--estado-error`.

## Tipografía

Fuente web gratuita de Google Fonts, sustituta de Helvetica Neue (la tipografía de apoyo del manual, que es de pago). `--fuente-base` cae a `"Helvetica Neue", Helvetica, Arial, sans-serif` si Inter no carga.

- `--fuente-base`: **Inter** 400, 500, 600 y 700.

| Uso | Tamaño | Peso |
|---|---|---|
| Título de pantalla | 32 px (28 px en móvil) | 700 |
| Título de sección | 24 px | 700 |
| Destacado y botones | 18 px | 600 |
| Texto general y campos | 16 px | 400 |
| Ayudas, fechas y etiquetas (mínimo) | 14 px | 400 o 500 |

Interlineado 1,5 (1,2 en títulos). Ningún texto por debajo de 14 px. Los campos de formulario usan 16 px para que el celular no haga zoom. El serif Baskerville del manual se reserva para el logotipo; no se usa en la interfaz.

## Espacio y forma

| Variable | Valor | Uso típico |
|---|---|---|
| `--espacio-1` | 4 px | Entre icono y texto |
| `--espacio-2` | 8 px | Entre etiqueta y campo |
| `--espacio-3` | 12 px | Relleno de botones |
| `--espacio-4` | 16 px | Entre campos y margen de página en móvil |
| `--espacio-5` | 24 px | Relleno de tarjetas |
| `--espacio-6` | 32 px | Entre secciones |
| `--espacio-7` | 48 px | Margen de página en escritorio |

- **Radios:** `--radio-control` 8 px (botones y campos); `--radio-tarjeta` 12 px (tarjetas y modales); `--radio-pastilla` 999 px (etiquetas de estado).
- **Sombra:** una sola, `--sombra-tarjeta`, muy suave, para tarjetas y el carrito flotante. Fuera de eso se separa con bordes de 1 px y espacio.
- **Área táctil:** todo elemento interactivo mide al menos 44 × 44 px.
- **Ancho:** móvil desde 360 px; la lista de ítems pasa de 1 a 2 y 3 columnas a 640 px y 1024 px.

## Tokens en CSS

Estas variables van en `client/src/styles/tokens.css` y se importan una sola vez en la entrada de la app:

```css
:root {
  /* Marca */
  --color-primario: #e11b22;
  --color-primario-hover: #b3151b;
  --color-enlace: #c41b1e;
  --color-texto: #231f20;
  --color-texto-secundario: #5c5f62;
  --color-fondo: #f5f5f5;
  --color-superficie: #ffffff;
  --color-borde: #d9dadb;
  --color-borde-campo: #767779;
  --color-foco: #1d4f91;

  /* Estados */
  --estado-ok: #1b6b3a;
  --estado-ok-fondo: #e3f3e8;
  --estado-aviso: #7a4a00;
  --estado-aviso-fondo: #fbf1df;
  --estado-error: #b3261e;
  --estado-error-fondo: #fbecea;
  --estado-info: #1d4f91;
  --estado-info-fondo: #e6eef8;
  --estado-neutro: #3f4245;
  --estado-neutro-fondo: #ecedee;

  /* Tipografía */
  --fuente-base: "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --texto-pantalla: 2rem;
  --texto-seccion: 1.5rem;
  --texto-destacado: 1.125rem;
  --texto-base: 1rem;
  --texto-ayuda: 0.875rem;

  /* Espacio */
  --espacio-1: 4px;
  --espacio-2: 8px;
  --espacio-3: 12px;
  --espacio-4: 16px;
  --espacio-5: 24px;
  --espacio-6: 32px;
  --espacio-7: 48px;

  /* Forma */
  --radio-control: 8px;
  --radio-tarjeta: 12px;
  --radio-pastilla: 999px;
  --sombra-tarjeta: 0 1px 3px rgba(35, 31, 32, 0.12);
  --area-tactil: 44px;
}
```

## Componentes

Todos usan solo variables. Toda lista, formulario o acción tiene los cuatro estados: **cargando**, **vacío**, **error** y **éxito**.

### Botones

| Tipo | Aspecto | Uso |
|---|---|---|
| Primario | Fondo `--color-primario`, texto blanco 18 px 600 | Una sola acción principal por pantalla (por ejemplo «Enviar solicitud») |
| Secundario | Fondo blanco, borde `--color-texto` 1 px, texto `--color-texto` | Acciones alternativas |
| Peligro | Fondo `--estado-error`, texto blanco | Cancelar reserva, bloquear perfil; siempre con confirmación |
| Texto | Sin borde, texto `--color-enlace` subrayado al hover | Acciones menores |

- Altura mínima 44 px; relleno `--espacio-3` × `--espacio-5`.
- Hover: primario pasa a `--color-primario-hover`. Foco: anillo de 3 px `--color-foco` con separación de 2 px.
- **Cargando:** el botón queda deshabilitado, muestra un indicador y cambia el texto a «Enviando…». No cambia de tamaño.
- **Deshabilitado:** fondo `--estado-neutro-fondo`, texto `--color-texto-secundario`, con la razón escrita al lado.

### Campos de formulario

- Etiqueta siempre visible arriba (no solo placeholder), 14 px 500. Borde 1 px `--color-borde-campo`, radio `--radio-control`, altura 44 px.
- Obligatorios se marcan con la palabra «(obligatorio)»; los opcionales, con «(opcional)». La nota del motivo es opcional.
- **Error:** borde y mensaje en `--estado-error`, con icono, debajo del campo y enlazado con `aria-describedby`. El mensaje dice qué pasó y cómo arreglarlo.
- **Éxito:** solo se confirma al enviar, no campo por campo.
- **Los cuatro estados en formularios:** cargando es el botón de envío (ver Botones); vacío son los campos sin llenar, con el botón primario deshabilitado y la razón («Falta: fecha de retiro»); error va en el campo; éxito, al enviar.

### Selector de fecha y horario (primer paso)

- Es lo primero que se ve al abrir el catálogo: fecha de retiro, hora de retiro, fecha de devolución y hora de devolución, más la duración («Menos de un mes» o «Durante el semestre»).
- Solo ofrece días de lunes a viernes y horas de 8:00 a 17:20. Los días y horas no válidos aparecen deshabilitados con el motivo («Fuera de horario de atención»).
- **Error:** «Elige una hora entre 8:00 y 17:20» y la devolución anterior al retiro.
- **Cargando:** los campos quedan deshabilitados con «Buscando disponibilidad…». **Vacío:** «No hay horarios libres ese día. Elige otra fecha.» **Éxito:** «Fecha y horario guardados.», con icono, al confirmar.

### Tarjeta de ítem o espacio

Foto general arriba (relación 4:3, con texto alternativo), nombre (18 px 600), una línea de detalle, etiqueta de estado y una acción.

- **Disponible:** botón «Agregar a la reserva».
- **No disponible** (también los ítems en mantenimiento, dañados o extraviados, que el estudiante ve igual): botón deshabilitado y la razón en texto «No disponible en este momento». Solo el administrador ve el estado exacto.
- **Con stock:** «3 de 5 disponibles». **Con unidad numerada (Oculus):** selector «Número de dispositivo».
- **Espacio (aulas, estudios, laboratorios):** si el usuario no es profesor, el botón no se muestra y aparece «Solo para profesores».
- **Cargando:** tarjetas esqueleto con las mismas medidas. **Vacío:** «No hay equipos disponibles en ese horario. Prueba otra fecha o franja.» con botón secundario «Cambiar fecha».
- **Error:** «No pudimos cargar los equipos. Revisa tu conexión.» con botón secundario «Reintentar».
- **Éxito:** al agregar un ítem, «Agregado a la reserva» con icono de check, en `role="status"`.

### Inicio de sesión y restablecimiento

- Campos de correo institucional y contraseña, con etiqueta visible. Botón primario «Entrar». Enlace «¿Olvidaste tu contraseña?».
- **Cargando:** el botón muestra «Entrando…». **Vacío:** con campos sin llenar, «Entrar» queda deshabilitado con la razón «Escribe tu correo y contraseña». **Error:** «Correo o contraseña incorrectos. Revisa los datos o restablece tu contraseña.» **Éxito:** al pedir el restablecimiento, «Te enviamos un enlace a tu correo institucional.»

### Calificación

- Cinco botones numerados del 1 al 5 (no estrellas, para que se usen con teclado y lector de pantalla), comentario opcional y botón primario «Enviar calificación». El estudiante califica la reserva al devolverla; el administrador califica el cumplimiento del usuario.
- **Cargando:** el botón muestra «Enviando…». **Vacío:** el botón queda deshabilitado con la razón «Elige una calificación de 1 a 5». **Error:** «No pudimos enviar tu calificación. Intenta de nuevo.» **Éxito:** «Gracias por calificar tu reserva.»

### Selector de idioma

- En el encabezado, un control «Español / English» con el idioma activo marcado. Cambia toda la interfaz y el atributo `lang`.
- **Cargando:** «Cambiando idioma…», solo por un instante. **Vacío:** no aplica, siempre hay dos idiomas. **Error:** «No pudimos cambiar el idioma. Sigue en español.» **Éxito:** «Idioma cambiado a English», anunciado con `role="status"`.

### Etiquetas de estado

Pastilla con icono + texto, 14 px 600, fondo y texto de la tabla de estados. Nunca solo el color.

**Estados de una reserva:**

| Estado | Variables | Icono | Texto (ES / EN) |
|---|---|---|---|
| En revisión | aviso | reloj | En revisión / Under review |
| Aprobada | ok | check | Aprobada / Approved |
| Rechazada | error | equis | Rechazada / Rejected |
| Retirada | info | caja | Retirada / Picked up |
| Devuelta | neutro | check doble | Devuelta / Returned |
| Cancelada | neutro | círculo tachado | Cancelada / Cancelled |
| Vencida | neutro | reloj tachado | Vencida (no retirada) / Expired |
| Devolución tardía | error, sólido: fondo `--estado-error`, texto blanco | alerta | Devolución tardía / Late return |

**Estados de un ítem:**

| Estado | Quién lo ve | Variables | Texto |
|---|---|---|---|
| Disponible | Todos | ok | Disponible |
| No disponible | Todos | neutro | No disponible |
| Mantenimiento | Solo administrador (al estudiante se le muestra «No disponible», igual que cualquier ítem no disponible) | aviso | Mantenimiento |
| Dañado | Solo administrador | error | Dañado |
| Extraviado | Solo administrador | neutro con borde `--estado-error` | Extraviado |

### Carrito

- En móvil es una barra fija inferior («3 ítems · Ver reserva») que abre una hoja; en escritorio es un panel lateral. Usa `--sombra-tarjeta`.
- Muestra cada ítem con fecha, hora y botón «Quitar»; sin límite de ítems.
- Aviso de caducidad: «Tu carrito se vacía 1 h después de agregar el último ítem si no envías la solicitud», con cuenta regresiva en los últimos 10 minutos.
- **Vacío:** «Tu carrito está vacío. Elige una fecha y agrega equipos.» **Error:** si un ítem dejó de estar libre, se marca con «Ya no está disponible en ese horario» y se ofrece quitarlo. Si no se pudo quitar un ítem por conexión: «No pudimos guardar el cambio. Intenta de nuevo.»
- **Cargando:** al quitar un ítem, su fila muestra «Quitando…» y se deshabilita.
- **Éxito:** al quitar, «Ítem quitado», con icono y en `role="status"`.
- **Éxito al enviar:** pantalla con el mensaje «Tu orden está siendo procesada, espera la aprobación», el número de la solicitud y la línea «Te avisaremos por correo y aquí».

### Panel del administrador

- Tabla de solicitudes en revisión con estudiante, ítems, fechas y acciones «Aprobar» (primario) y «Rechazar» (secundario). Al abrir una solicitud puede quitar ítems o modificar el carrito.
- En pantallas menores a 640 px cada fila se vuelve una tarjeta. Los botones de aprobar y rechazar no quedan a menos de 8 px entre sí.
- **Cargando:** filas esqueleto con las mismas medidas. **Error:** «No pudimos cargar las solicitudes.» con botón secundario «Reintentar».
- **Vacío:** «No hay solicitudes pendientes.» **Éxito:** «Reserva aprobada. Se envió el comprobante a [número] destinatarios.»
- **Editar carrito:** botón secundario «Editar carrito» abre un diálogo con los ítems de la reserva y el campo **Motivo del cambio (obligatorio)**. Mientras el campo esté vacío, «Guardar cambio» queda deshabilitado con la razón «Escribe el motivo del cambio». Al guardar: «Cambio guardado. El estudiante recibió un aviso con el motivo.» **Error:** «No pudimos guardar el cambio. Intenta de nuevo.»

### Mensajes y notificaciones

- Mensaje en pantalla: bloque con icono, fondo del estado, texto 16 px, radio `--radio-tarjeta`, `role="status"` (o `role="alert"` para errores).
- Toda notificación por correo se muestra también dentro de la aplicación, con fecha y estado de envío.
- Confirmación obligatoria antes de cancelar, bloquear o dar de baja: título, consecuencia en una frase y botones «Volver» y la acción.

## Datos y textos

| Dato | Formato | Ejemplo |
|---|---|---|
| Fecha | día abreviado, número y mes abreviado; año solo si no es el actual | `mié 2 dic` |
| Hora | 24 horas, hora de Quito | `8:00` |
| Rango | inicio a fin con raya | `mié 2 dic · 8:00–12:00` |
| Rango de varios días | fecha y hora de cada extremo | `lun 7 dic 8:00 → vie 11 dic 17:00` |
| Cantidad | «N de M disponibles» | `3 de 5 disponibles` |
| Unidad numerada | «Dispositivo N» | `Dispositivo 2` |
| Números | punto para miles y coma para decimales | `1.250`, `4,5` |
| Identificador de reserva | `R-` y número de 5 cifras | `R-00482` |
| Plazos | siempre con unidad y fecha exacta cuando existe | «Cancela hasta las 7:00 de hoy» |

En inglés se usan los mismos formatos con los textos traducidos; las horas siguen en 24 horas.

## Tono de voz

Directo, amable y concreto. Se habla de «tú». Se dice qué pasó y qué sigue. Sin jerga técnica ni culpa.

| Así sí | Así no |
|---|---|
| Tu solicitud está en revisión. Te avisaremos por correo. | Solicitud pendiente de procesamiento. |
| Esa cámara ya está reservada de 10:00 a 12:00. Prueba otro horario. | Error 409: conflicto. |
| Pasaron 15 minutos. Acércate a retirar tu reserva antes de las 8:30. | ¡Llegas tarde! |
| Tienes un bloqueo hasta el 9 de diciembre por una devolución tardía. | Usuario sancionado. |
| Solo los profesores pueden reservar este espacio. | Acceso denegado. |

## Accesibilidad

- Contraste de 4,5:1 o más en todo texto y 3:1 en bordes de campos y componentes (verificado con la paleta de este archivo).
- Todo se puede usar con teclado; el foco siempre es visible. El orden de tabulación sigue el orden visual.
- Estado, error y éxito nunca dependen solo del color: llevan icono y texto.
- Cada campo tiene etiqueta; los errores se anuncian con `role="alert"`; las imágenes tienen texto alternativo.
- Áreas táctiles de 44 px mínimo; el contenido funciona al 200 % de zoom y desde 360 px de ancho.
- Atributo `lang` según el idioma elegido (`es` o `en`). Se respeta `prefers-reduced-motion`.

## No hacemos

- No usamos rojo para errores ni como único indicador de estado.
- No ponemos más de un botón primario por pantalla.
- No escribimos colores, tamaños ni espacios sueltos fuera de las variables.
- No usamos el escudo clásico en la interfaz: solo el logotipo con las siglas (el escudo es para documentos oficiales).
- No usamos Baskerville ni University Roman en la interfaz (solo en el logotipo).
- No mostramos los estados internos (mantenimiento, dañado, extraviado) a estudiantes ni profesores.
- No limitamos el número de ítems del carrito ni de reservas por usuario (regla del cliente).
- No ofrecemos renovar reservas ni chatbot (fuera de alcance).
- No ponemos texto dentro de imágenes ni mensajes que culpen al usuario.
