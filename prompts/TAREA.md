Tarea: Mi prompt avanzado
Herramienta de IA usada: ChatGPT

Tarea elegida
Generar casos de prueba para un formulario de registro de usuarios con los campos nombre, correo y contraseña , donde no se permiten correos repetidos. Es una tarea util en desarrollo de software porque los casos de prueba se pueden pasar directo a una hoja de calculo o a una herramienta de QA.

Version 1: prompt basico
text
Dame casos de prueba para un registro de usuarios.
Tecnica agregada: ninguna fue un prompt basico de una sola instruccion.

Por que: para tener un punto de partida y ver que hace la IA sin ninguna guia.

Que paso en la respuesta: la IA entrego una tabla de 30 casos mas una lista de casos adicionales. Fue demasiado largo, sin una cantidad ni un formato que yo hubiera definido. Como no le di las reglas del formulario, asumio todo por su cuenta y varios resultados esperados quedaron genericos ("segun especificacion", "se acepta").

Version 2
text
Actua como analista de pruebas de software (QA) especializado en formularios web.
Escribe 8 casos de prueba para un formulario de registro de usuarios con los campos: nombre, correo y contraseña.
Responde en una tabla con las columnas: ID, escenario, datos de entrada, resultado esperado.
Responde en espanol.
Tecnicas agregadas: role prompting y formato definido (cantidad exacta y columnas de la tabla).

Por que: en la v1 la respuesta fue larga y sin estructura. Con un rol concreto y un formato claro, la IA sabe desde que punto de vista responder y como entregar el resultado.

Que mejoro: salieron exactamente 8 casos en una tabla con las columnas pedidas. Uso mis campos y la regla del minimo de 8 caracteres. Que todavia fallaba: aparecian etiquetas <br> dentro de las celdas, no habia casos de seguridad ni de limites extremos y la IA no reviso su propia tabla.

Version 3: prompt final
text
<rol>Actua como analista de pruebas de software (QA) senior especializado en formularios web de registro.</rol>
<contexto>Formulario de registro con los campos: nombre, correo y contraseña. No permite correos repetidos.</contexto>
<tarea>
1. Piensa paso a paso que puede fallar en este formulario.
2. Escribe 8 casos de prueba.
3. Revisa tu tabla: si falta algun caso limite o de seguridad, agregalo e indica cuales agregaste.
</tarea>
<ejemplo>
TC-01 | Registro exitoso | Nombre: Ana Lopez; Correo: ana@mail.com; Contrasena: Clave1234 | Se crea la cuenta y se muestra mensaje de exito
</ejemplo>
<formato>Tabla con las columnas: ID, escenario, datos de entrada, resultado esperado. Usa el mismo estilo del ejemplo. No uses etiquetas HTML como <br>. Responde en espanol.</formato>
Tecnicas agregadas: prompt estructurado, chain of thought,few-shot, autocritica y un rol mas especifico (QA senior en formularios de registro).

Por que: la v2 no cubria seguridad ni casos limite, asi que agregue autocritica y chain of thought para que la IA buscara lo que faltaba. Agregue el ejemplo para fijar el estilo de las filas y las etiquetas para que las partes del prompt no se mezclen. Tambien prohibi el <br> para corregir el defecto de la v2.

Que mejoro: la IA escribio primero una tabla de 8 casos. Luego, en la revision, agrego dos casos de seguridad: TC-09  y TC-10. Uso mi ejemplo como estilo (Nombre: Ana Lopez; Correo: ana@mail.com) y ya no aparecieron etiquetas <br> en lo que se ve en la captura.

Tecnicas usadas en el prompt final
Parte del prompt final	Tecnica
<rol>Actua como analista de pruebas de software (QA) senior...</rol>	Role prompting
Etiquetas <rol>, <contexto>, <tarea>, <ejemplo>, <formato>	Prompt estructurado
"Piensa paso a paso que puede fallar en este formulario"	Chain of thought
<ejemplo>TC-01 | Registro exitoso | ...</ejemplo>	Few-shot (un ejemplo de fila)
"Revisa tu tabla: si falta algun caso limite o de seguridad, agregalo e indica cuales agregaste"	Autocritica
<formato>Tabla con las columnas: ID, escenario, datos de entrada, resultado esperado...</formato>	Formato de respuesta definido
Evaluacion del resultado
Criterio	Cumple (Si / No)
La respuesta usa las 4 columnas pedidas (ID, escenario, datos de entrada, resultado esperado)	Si
Incluye casos con campos vacios	Si
Incluye casos de seguridad 	Si
Incluye el limite de la contrasena 	Si
Indica que casos agrego en la autocritica	Si
No aparecen etiquetas <br> en la tabla	Si
La lista de casos agregados es correcta y no repite casos	No
Observacion propia: en la autocritica la IA dijo que agrego TC-05, TC-09 y TC-10, pero TC-05 ya estaba en la tabla inicial de 8 casos. Solo TC-09 y TC-10 fueron realmente nuevos. La IA tambien puede equivocarse al revisarse, por eso yo soy el ultimo revisor.

Por que elegi estas tecnicas
Elegi role prompting y prompt estructurado porque los casos de prueba necesitan el punto de vista de un analista QA y un formato fijo de tabla. Las etiquetas evitan que el rol, las reglas del formulario y el formato se mezclen. Use chain of thought porque probar un formulario exige pensar primero que puede fallar y despues escribir los casos. Agregue un ejemplo para que todas las filas tuvieran el mismo estilo y se puedan copiar a Excel sin corregirlas. Agregue autocritica porque en la v2 faltaban casos de seguridad y la revision permitio completarlos. No use descomposicion porque la tarea es pequena y no necesita dividirse en varios pedidos; en cambio, dividirla habria hecho el proceso mas largo sin mejorar el resultado.

