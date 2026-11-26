# Plataforma Web de Reservas de Equipos y Espacios — PRD del MVP

**Equipo:** Andrés Merino, Mateo Gordon, Pablo Vargas
**Cliente:** Área administrativa de la facultad (Santiago, administrador, y su jefe Luis Daniel)
**Versión:** Avance 2 — noviembre de 2026

> **Convenciones de trazabilidad.** `[D#]` = decisión del cliente en la visita (sección 6). `[S#]` = supuesto del equipo (sección 7). `[P#]` = pregunta abierta (sección 7). Los números usan punto para miles y coma para decimales; los montos están en USD.

---

## 1. Problema y objetivo

**Problema.** El sistema actual de préstamo de equipos (cámaras de cine, periodismo y comunicación) y de reserva de espacios (estudio de TV Miguel de Santiago, laboratorios) falla de forma crítica: borra el carrito al agregar más de un producto, no restablece contraseñas y no envía correos de confirmación. Como no hay aprobación inmediata, las reservas se sobrelapan [D3]. Santiago atiende las reservas a mano y no le queda tiempo para otras tareas.

**Objetivo.** Que el estudiante reserve varios equipos o un espacio de forma autónoma, en pocos pasos, sin sobrelapes, y que el administrador apruebe, rechace y controle todo desde un solo panel, con notificaciones que lleguen y comprobantes de cada reserva.

---

## 2. Usuarios

| Perfil | Quién es | Qué necesita hacer |
|---|---|---|
| **Estudiante** | Usuario final con perfil creado por el administrador [D18] | Elegir fecha y horario, explorar el catálogo, armar un carrito con varios ítems, enviar la solicitud, seguir su estado, cancelar, recibir notificaciones y ver su historial. |
| **Profesor** | Usuario con perfil de estudiante, distinguido por una nota del administrador [D17] | Lo mismo que el estudiante y, además, reservar espacios (aulas, estudios, laboratorios). |
| **Administrador** | Santiago, Luis Daniel; mínimo dos perfiles [D18] | Gestionar catálogo y disponibilidad, aprobar o rechazar reservas completas, quitar ítems o modificar carritos, cancelar por incumplimiento, crear usuarios, poner notas, bloquear perfiles, definir contactos de seguridad y obtener reportes. |
| **Seguridad** (destinatario, sin cuenta) | Persona(s) que el administrador designa | Recibir el comprobante de cada reserva aprobada [D4]. |

---

## 3. Alcance del MVP

1. Iniciar sesión con correo institucional y restablecer la contraseña.
2. Elegir primero la fecha y el horario, y ver solo lo disponible en ese rango [D2].
3. Explorar el catálogo de equipos y espacios con foto general, descripción y estado [D16].
4. Agregar a un carrito sin límite de ítems, que se vacía por completo 1 hora después de agregar el último ítem si la solicitud no se envió [D1, D11].
5. Seleccionar la duración de la reserva (menos de un mes o durante el semestre) y añadir una nota con el motivo [D5].
6. Para ítems con unidades numeradas (por ejemplo Oculus), elegir el número de dispositivo; para ítems con stock, asignar automáticamente una unidad libre [D16, S1].
7. Enviar la solicitud y ver el mensaje «Tu orden está siendo procesada, espera la aprobación» [D4].
8. Aprobar o rechazar la reserva completa, pudiendo quitar ítems o modificar el carrito [D3].
9. Generar un comprobante digital al aprobar y enviarlo al estudiante y a los contactos de seguridad [D4].
10. Cancelar una reserva hasta 1 hora antes de su inicio, y que el administrador cancele por incumplimiento [D9].
11. Cancelar automáticamente una reserva no retirada a los 30 minutos y notificarlo [D8].
12. Bloquear automáticamente por 2 semanas a quien devuelva tarde o incumpla, y permitir al administrador bloquear perfiles [D13].
13. Gestionar el catálogo: crear, editar y dar de baja ítems y espacios, con fotos, detalles y estados [D14, D15, D18].
14. Configurar horarios de disponibilidad globales o por equipo, incluidas excepciones [D6].
15. Crear y dar de baja usuarios y escribir notas en su perfil [D17, D18].
16. Enviar notificaciones por correo y dentro de la aplicación: solicitud recibida, aprobada, rechazada, aviso de retiro, cancelación, recordatorio de devolución, equipo dañado y recordatorio mensual de mantenimiento para el administrador [D15, D21].
17. Calificar la experiencia: el estudiante califica el servicio y el administrador califica al usuario [D19, S5].
18. Reportes exportables a Excel: reserva (comprobante), ítems más rentados al fin de semestre y lo rentado por usuario [D20].
19. Interfaz responsive, en español e inglés [D22].
20. Modificar el carrito o la reserva de un estudiante (quitar, agregar o cambiar ítems y fechas), con una nota obligatoria del motivo. El estudiante recibe un aviso con el cambio y el motivo [S15].

---

## 4. Reglas de negocio

**Horarios y plazos**

1. Retiros y devoluciones solo de lunes a viernes, de 8:00 a 17:20 (hora de Quito). Fuera de ese horario no se permiten [D6].
2. El administrador puede definir excepciones de horario por equipo (por ejemplo, computadores de edición) [D6, S3].
3. Entre dos reservas del mismo ítem o espacio debe haber al menos 30 minutos de separación [D7].
4. Una reserva no retirada genera un aviso al estudiante a los 15 minutos de iniciada y se cancela automáticamente a los 30 minutos, con notificación [D8].
5. El estudiante puede cancelar hasta 1 hora antes del inicio; después ya no puede [D9].
6. No hay renovación de reservas; para extender se debe crear una nueva [D10].

**Duración y carrito**

7. Toda reserva declara una de dos duraciones: «menos de un mes» o «durante el semestre». El máximo es un semestre [D5].
8. No se exige justificar una duración larga; la nota del motivo es opcional [D5, S6].
9. El carrito no tiene límite de ítems. Si pasan 1 hora desde que se agregó el último ítem y la solicitud no se envió, el carrito se vacía por completo [D1, D11].
10. No existe límite de reservas por usuario [D12].

**Disponibilidad y asignación**

11. Un ítem no puede estar en dos reservas aprobadas que se crucen en tiempo, incluida la separación de 30 minutos [D7].
12. Para ítems con stock, el sistema asigna cualquier unidad libre; para ítems como Oculus hay un solo ítem en el catálogo y el estudiante elige el número de dispositivo [D16, S1].
13. Los laboratorios son espacios y los computadores son ítems de reserva [D17].
14. Los espacios (aulas, estudios, laboratorios) solo pueden ser reservados por perfiles con la nota «Profesor» [D17].

**Estados de un ítem**

15. Un ítem tiene cinco estados: **disponible** y **no disponible**, visibles para todos; **mantenimiento**, **dañado** y **extraviado**, visibles solo para el administrador [D14].
16. Un ítem en mantenimiento no sale del catálogo: se muestra a los estudiantes como «No disponible», con el mismo texto que cualquier ítem no disponible [D15, S2].
17. Solo el administrador cambia las etiquetas de estado, y el sistema le envía un recordatorio mensual para revisar los ítems en mantenimiento [D15].

**Estados de una reserva** (definidos por el equipo a partir de las reglas anteriores) [S4]

18. Una reserva pasa por estos estados: **En revisión** → **Aprobada** o **Rechazada**; una aprobada puede pasar a **Retirada** → **Devuelta**, o a **Cancelada** (por el estudiante, por el administrador o automática) o **Vencida** (no retirada a los 30 minutos); si no se devuelve a tiempo pasa a **Devolución tardía**.
19. El administrador aprueba o rechaza la reserva completa, y puede quitar ítems o modificar el carrito antes de aprobar [D3].
20. Una reserva aprobada genera un comprobante digital con identificador único, que se envía al estudiante y a los contactos de seguridad definidos por el administrador [D4, D20].

**Sanciones y daños**

21. Una devolución tardía o un incumplimiento genera un bloqueo automático de 2 semanas para crear nuevas reservas [D13, S7].
22. El administrador puede bloquear o desbloquear un perfil manualmente, por ejemplo ante un equipo dañado; la resolución del daño ocurre fuera de la plataforma [D13].
23. Si un equipo se declara dañado, el sistema lo notifica [D21, P6].

**Cuentas y notificaciones**

24. Solo el administrador crea y da de baja perfiles; no hay registro abierto [D18].
25. Debe haber como mínimo dos perfiles de administrador activos [D18].
26. Las notas de un perfil solo las agrega y edita el administrador; el estudiante no las ve [D17, S8].
27. Toda notificación se envía por correo y se muestra también dentro de la aplicación para asegurar que llegue [D21, S9].
28. El administrador puede modificar el carrito o la reserva de un estudiante en revisión o aprobada. Cada cambio exige una nota del motivo, que queda guardada en el historial de la reserva [S15].

---

## 5. Fuera de alcance

| Elemento | Por qué queda fuera |
|---|---|
| Chatbot de ayuda | El cliente confirmó que está fuera de alcance [D19]. |
| Renovación de reservas | El cliente indicó que no habrá sistema de renovación [D10]. |
| Gestión de daños, cobros o multas | Los daños se resuelven fuera de la plataforma; solo se bloquea el perfil [D13]. |
| Integración con el servidor SMTP o el Active Directory de la universidad | El administrador crea los perfiles, así que no se valida contra un servidor externo [D18, S10]. |
| Límite de reservas por usuario | El cliente indicó que no existe [D12]. |
| Pagos o cobro real | El «comprobante» o «factura» es un registro de la reserva, no un cobro [S11]. |
| Aplicación móvil nativa | Se cubre con diseño responsive [D22]. |
| Carga de fotos individuales por unidad | Se usan fotos generales por ítem [D16]. |

---

## 6. Decisiones del cliente

Todas se tomaron en la visita en clase del **miércoles 11 de noviembre de 2026**.

| N.º | Decisión | Fecha | Efecto |
|---|---|---|---|
| D1 | La experiencia de reserva debe parecerse a Amazon: varios ítems en una sola reserva y sin límite de ítems en el carrito. | 11 nov 2026 | Cambió el carrito |
| D2 | Elegir la fecha antes de ver los productos, como en Airbnb, con la menor cantidad de pasos posible. Hoy los usuarios tienen problemas para visualizar fechas. | 11 nov 2026 | Define el flujo |
| D3 | Todas las reservas requieren aprobación manual. El administrador aprueba la reserva completa y puede eliminar ítems o modificar el carrito. | 11 nov 2026 | Confirmó |
| D4 | Al finalizar el pedido se muestra «Tu orden está siendo procesada, espera la aprobación». Al aprobar se genera un comprobante digital que se envía a seguridad. | 11 nov 2026 | Definió |
| D5 | Hay dos duraciones: menos de un mes y durante el semestre. No se exige razón para plazos largos, pero sí una nota del motivo. | 11 nov 2026 | Definió |
| D6 | Horario de 8:00 a 17:20, de lunes a viernes. Retiros y devoluciones solo en horario. Hay equipos con excepciones (computadores de edición) y otros que no pueden registrarse a las 4 a. m. | 11 nov 2026 | Definió |
| D7 | Separación de 30 minutos entre reservas. | 11 nov 2026 | Definió |
| D8 | Aviso a los 15 minutos de retraso en el retiro y cancelación a los 30. | 11 nov 2026 | Aclaró el «15-30 min» |
| D9 | El estudiante cancela hasta 1 hora antes. El administrador cancela manualmente a quien no llega pasado el tiempo de gracia. | 11 nov 2026 | Definió |
| D10 | No hay sistema de renovar reservas. | 11 nov 2026 | Excluyó |
| D11 | Los ítems del carrito se eliminan a la hora si no se completó la reserva. Aclaración del equipo: el plazo cuenta desde el último ítem agregado y el carrito se vacía por completo. | 11 nov 2026 | Definió |
| D12 | No existe límite de reservas por usuario. | 11 nov 2026 | Confirmó |
| D13 | Devolución tardía o incumplimiento: bloqueo automático de 2 semanas. Los daños se resuelven fuera de la página, pero el administrador puede bloquear el perfil. | 11 nov 2026 | Respondió la pregunta de sanciones |
| D14 | Cinco estados de ítem: disponible y no disponible (todos), mantenimiento, dañado y extraviado (solo administrador). | 11 nov 2026 | Definió |
| D15 | Un ítem en mantenimiento no se elimina: muestra una nota. Solo el administrador cambia las etiquetas y recibe recordatorios mensuales. | 11 nov 2026 | Definió |
| D16 | Para ítems como Oculus hay un solo ítem con elección de número de dispositivo. Se usan fotos generales y se deben diferenciar los ítems. | 11 nov 2026 | Respondió la pregunta de unidades |
| D17 | Los laboratorios son espacios y los computadores son ítems. Los espacios son solo para profesores. Profesores y estudiantes comparten tipo de perfil y se distinguen por notas del administrador. | 11 nov 2026 | Definió |
| D18 | El administrador crea los perfiles de usuario, modifica el catálogo y controla toda la disponibilidad. Debe haber al menos dos administradores. | 11 nov 2026 | Respondió la pregunta de autenticación |
| D19 | La calificación es parte del MVP. El chatbot queda fuera. | 11 nov 2026 | Incluyó / excluyó |
| D20 | Cada reserva genera un reporte (factura). Al final del semestre hay un reporte de los ítems más rentados y otro de cada usuario y lo que rentó. | 11 nov 2026 | Definió |
| D21 | Las notificaciones deben llegar al estudiante, incluida una notificación de devolución. Se notifica si un equipo está dañado. | 11 nov 2026 | Definió |
| D22 | Responsive es importante; la página debe estar en español e inglés; se construye en React; hay que seguir el manual de marca de la universidad. | 11 nov 2026 | Restricción |

---

## 7. Supuestos y preguntas abiertas

### Supuestos

| N.º | Supuesto (se usa mientras nadie lo confirme) |
|---|---|
| S1 | Los ítems con stock (por ejemplo, cinco cámaras iguales) se reservan por modelo y el sistema asigna una unidad libre; los de unidad numerada (Oculus) se eligen por número. |
| S2 | Un ítem en mantenimiento, dañado o extraviado aparece para el estudiante como «No disponible», con el mismo texto que cualquier ítem no disponible. Solo el administrador ve el estado exacto y la nota de mantenimiento. Respuesta del equipo en la visita. |
| S3 | Las excepciones de horario por equipo las configura el administrador; el sistema no impone ninguna por defecto. |
| S4 | Los nombres y las transiciones de los estados de una reserva (regla 18) son propuesta del equipo: el cliente no los definió. |
| S5 | La calificación consiste en una puntuación de 1 a 5 con comentario opcional: el estudiante califica la reserva al devolver y el administrador califica el cumplimiento del usuario. |
| S6 | La nota del motivo es opcional para todas las reservas. |
| S7 | El «incumplimiento» incluye no retirar la reserva a los 30 minutos. El bloqueo impide crear nuevas reservas, pero respeta las ya aprobadas. |
| S8 | Las notas de perfil son internas y el estudiante no las ve. |
| S9 | «Asegurar que lleguen» se cubre con correo más aviso dentro de la aplicación y registro del envío. |
| S10 | El correo institucional es el identificador de la cuenta; la contraseña se gestiona dentro del sistema, con restablecimiento propio. |
| S11 | El comprobante (factura) no tiene valor monetario ni tributario. |
| S12 | El recordatorio de devolución se envía 1 hora antes de la hora de devolución. |
| S13 | El presupuesto de operación se planifica con el valor más alto citado (USD 150 al mes) y se prefiere software y servicios gratuitos. |
| S14 | Cada reserva tiene un único espacio o varios ítems; la reserva de un estudio no incluye automáticamente su equipamiento. |
| S15 | Confirmado por el equipo: el administrador puede modificar el carrito o la reserva de un estudiante (agregar, quitar o cambiar ítems y fechas) en revisión o aprobada. Cada cambio exige una nota del motivo, guardada en el historial, y el estudiante recibe un aviso con el cambio y el motivo. |

### Preguntas abiertas

| N.º | Pregunta | Supuesto mientras tanto |
|---|---|---|
| P1 | **Antelación.** El cliente indicó que no hay tiempo previo mínimo de reserva, y que se cancela hasta 1 hora antes. ¿Hay un máximo de antelación para reservar? | Se puede reservar con cualquier fecha futura dentro del semestre en curso. Se descartó interpretar que solo se puede reservar con 1 hora de antelación porque contradice D2 y D5. |
| P2 | ¿Cuál es el presupuesto real de hosting y correo, USD 1,50 o USD 150 al mes? (Contradicción entre los resúmenes 2 y 1, 3, 5.) | S13. |
| P3 | ¿Qué espacio o equipo tiene excepciones de horario y cuáles son? | S3. |
| P4 | ¿Qué campos lleva el reporte Excel? | Estudiante, ítem, fecha y hora de retiro y devolución, duración, estado y nota del motivo. |
| P5 | ¿Quién toma las fotos del inventario inicial? | Se usan las fotos generales que entregue el cliente junto al Excel; si no hay, un marcador de imagen. |
| P6 | ¿A quién se notifica un equipo dañado: al administrador, al último usuario o a ambos? | Al administrador y al último usuario que lo tuvo. |
| P7 | ¿Cuánto dura el bloqueo del administrador por daño y puede el estudiante apelar? | No tiene duración fija: lo levanta el administrador. |
| P8 | ¿Un profesor puede reservar equipos además de espacios, y se le aplica el mismo bloqueo? | Sí a ambas. |
| P9 | ¿El cliente aprueba los estados de reserva de S4? | Se usan los de la regla 18. |
| P10 | ¿El estudiante debe ver la nota del motivo de un cambio hecho por el administrador, o basta con el aviso? | **Resuelta:** sí la ve, dentro del aviso. |

---

## 8. Épicas del MVP

| Épica | Descripción |
|---|---|
| **E1. Catálogo y disponibilidad** | Ítems y espacios con fotos, estados, horarios globales o por equipo y consulta por fecha primero. |
| **E2. Carrito y solicitud de reserva** | Elegir fecha, armar el carrito sin límite, expiración a la hora, duración, nota, asignación de unidades y envío de la solicitud. |
| **E3. Aprobación y ciclo de la reserva** | Revisión del administrador, edición del carrito, retiro, devolución, cancelaciones y vencimiento automático. |
| **E4. Cuentas, perfiles y sanciones** | Creación de usuarios por el administrador, notas, perfiles profesor y estudiante, bloqueos y calificaciones. |
| **E5. Notificaciones, comprobantes y reportes** | Correos y avisos, comprobante digital, envío a seguridad y reportes en Excel. |

---

## 9. Criterios de éxito y restricciones

### Criterios de éxito

- El estudiante completa una reserva (fecha, ítems, envío) sin que el carrito se borre. [S, a validar con el cliente]
- No existen sobrelapes de ítems entre reservas aprobadas.
- Santiago deja de atender reservas manualmente: aprueba, rechaza o corrige desde el panel.
- Toda reserva aprobada genera comprobante y notificación al estudiante y a seguridad.
- Al fin de semestre el administrador exporta el reporte de ítems más rentados.

### Restricciones

- **Fecha:** documentos del avance 2 el 25 de noviembre; construcción en el avance 3 el 2 de diciembre; presentación final al cliente.
- **Tecnología:** React [D22].
- **Marca:** seguir el manual de marca de la universidad [D22].
- **Datos existentes:** el inventario inicial llega en un archivo de Excel y hay que cargarlo.
- **Idioma y dispositivos:** español e inglés; responsive, con prioridad en móvil [D22].
- **Despliegue y presupuesto:** por confirmar (P2).

---

## 10. Uso de IA

El equipo usó Claude (Anthropic) para: reunir en un solo lugar las respuestas de la visita, ordenar las decisiones y asignarles un número, proponer los estados de reserva (S4) y detectar contradicciones, como la de la antelación (P1), la del plazo de retiro («15-30 min») y la del límite de reserva. También se usó para redactar este borrador.

El grupo revisó en conjunto el documento durante una llamada grupal. Cuando algo contradecía lo que dijo el cliente, se priorizó su respuesta.
