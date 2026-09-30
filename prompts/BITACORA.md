# Bitacora de tecnicas avanzadas

Laboratorio 07: Tecnicas Avanzadas de Prompting.
Herramienta de IA usada: Chat GPT

## Ejercicio 2: Zero-shot, one-shot y few-shot

Clasifique 5 comentarios de clientes con tres tipos de prompt, cada uno en un chat nuevo.

| Tipo | Aciertos | Formato de la respuesta | Todas con el mismo formato (Si/No) |
|------|-----------------|-------------------------|------------------------------------|
| Zero-shot | 5 | Libre: una vez salio como tabla y otra como lista con el comentario y la etiqueta | No |
| One-shot | 5 | Lista numerada con solo la etiqueta | Si |
| Few-shot | 5 | Linea por linea: "texto" -> etiqueta | Si |

Observacion: las tres versiones acertaron las 5 etiquetas la diferencia estuvo en el formato: en zero-shot la IA eligio uno distinto cada vez, en one-shot uso una lista simple y en few-shot copio exactamente el formato de los ejemplos.

## Ejercicio 3: Chain of Thought

Resolvi el mismo problema de precios de dos maneras, cada una en un chat nuevo. Compare los resultados con la calculadora.

| Paso | Calculo | Resultado |
|------|---------|-----------|
| 1. Precio con descuento | 120 x 0,75 | 90 |
| 2. Precio con IGV | 90 x 1,18 | 106,20 |
| 3. Total por 3 unidades | 106,20 x 3 | 318,60 |

| Pedido | Respuesta de la IA | Muestra los pasos (Si/No) | Correcta (Si/No) |
|--------|--------------------|---------------------------|------------------|
| Directo | 318.60 | No | Si |
| Paso a paso | S/ 318.60 | Si | Si |

Por que es util ver el razonamiento aunque la respuesta directa haya sido correcta:
En el pedido directo solo vi un numero y tuve que creerle a la IA o recalcular todo por mi cuenta. En el paso a paso pude comparar cada calculo con mi calculadora y, si hubiera un error, saber exactamente en que paso fallo.

## Ejercicio 4: Role prompting

Hice la misma pregunta ("Explica que es una variable en programacion") con tres versiones, cada una en un chat nuevo.

| Version | Vocabulario  | Usa ejemplos o codigo | A quien le sirve mas |
|---------|-------------------------------|-----------------------|----------------------|
| A. Sin rol | Sencillo y general | Si, ejemplo corto en Python y la comparacion de la caja con etiqueta | A cualquier persona que quiere una idea rapida |
| B. Rol docente | Sencillo, con comparaciones de la vida diaria | Si, varios ejemplos en Python paso a paso (print, tipos de datos, cambio de valor) | A estudiantes que nunca han programado |
| C. Rol senior | Tecnico: tipo de dato, memoria, tipado fuerte, referencia y objeto | Si, codigo Java (int edad = 30; System.out.println) | A un companero que ya programa y quiere precision tecnica |

Observacion: el rol no le dio conocimientos nuevos a la IA, cambio el enfoque, el vocabulario y el nivel de detalle. En B uso la comparacion de la caja con etiqueta y lenguaje simple; en C uso Java y conceptos como tipado fuerte y referencias.

## Ejercicio 5: Descomposicion

Compare un pedido de una sola vez con un pedido dividido en 4 pasos, todos en el mismo chat.

- Paso 1: la IA listo 5 requisitos: gestion de productos, control de existencias, alertas de stock bajo, busqueda y consultas, y reportes de inventario.
- Paso 2: con esos requisitos diseno 5 clases, cada una con sus atributos y tipos de dato, mas un enum TipoMovimiento y un esquema de relaciones.
- Paso 3: escribio la clase Producto con los atributos del diseno como el codigo, nombre, categoria, precio, stockActual, stockMinimo, un constructor y los metodos get y set.
- Paso 4: propuso 3 mejoras: validar datos en el constructor y setters, usar BigDecimal para el precio y agregar el metodo tieneStockBajo().

Comparacion con el pedido de una sola vez:En el pedido por pasos pude revisar cada parte antes de seguir y el codigo de Producto fue coherente con el diseno de clases, que a su vez salio de los requisitos.

Compilacion opcional (javac Producto.java): (escribe aqui si lo hiciste y si compilo sin errores, o "no realizado").

## Ejercicio 6: Prompt estructurado y autocritica

Probe un prompt basico y uno estructurado, cada uno en un chat nuevo. Luego pedi una autocritica en el mismo chat del prompt estructurado.

Prompt basico: "Dame casos de prueba para un login." La IA respondio con una tabla de 25 casos mas una lista de casos limite. Fue muy largo y sin un formato que yo hubiera definido.

Prompt estructurado: la IA entrego una tabla de 6 casos (TC-01 a TC-06) con las 4 columnas pedidas. Cubre el inicio de sesion valido, los tres intentos fallidos consecutivos, el acceso despues del bloqueo y un intento fallido sobre una cuenta ya bloqueada.

Autocritica: la IA mantuvo los 6 casos y agrego 5: TC-07 (correo y contrasena vacios), TC-08 (correo vacio), TC-09 (contrasena vacia), TC-10 (correo con formato invalido) y TC-11 (contrasena con espacios). Tambien indico cuales agrego.

| Que revisar | Cumple (Si / No) |
|-------------|------------------|
| Tiene las 4 columnas pedidas? | Si |
| Incluye el bloqueo despues de 3 intentos? | Si |
| Incluye casos con campos vacios? | Si |
| Indica que casos agrego en la autocritica? | Si |
| Hay algun caso repetido o que no tenga sentido? | No |

Observaciones propias: TC-07, TC-08 y TC-09 se parecen entre si, y en TC-11 el resultado esperado quedo ambiguo (dice "si estan prohibidos... si estan permitidos..."). La IA tambien puede equivocarse al revisarse, por eso yo soy el ultimo revisor.

Prompt usado:

```text
<rol>Actua como analista de pruebas de software.</rol>
<contexto>Login web con correo y contrasena. La cuenta se bloquea
despues de 3 intentos fallidos.</contexto>
<tarea>Piensa paso a paso que puede fallar y escribe 6 casos de prueba.</tarea>
<formato>Tabla con las columnas: ID, escenario, datos de entrada,
resultado esperado.</formato>

Revisa tu tabla: faltan casos limite como campos vacios, correo sin @
o contrasena con espacios? Agrega los que falten e indica cuales agregaste.
```