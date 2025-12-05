# Una breve pasada por el flujo general del proceso


![Agente Principal]


1. El usuario envía un mensaje al bot en Telegram; ese es el Trigger.

2. Un node Set separa dos campos de datos: message y chat_ID.

3. El Agente Principal del workflow es el responsable de interactuar con el usuario y llamar a los subworkflows para obtener la información necesaria.
Este Agente no sabe nada sobre muebles, precios, variaciones, etc. Para conocer los precios consulta al agente
ConsultaPrecios; para registrar el presupuesto llama al agente Registro de Presupuesto; y para generar el documento en PDF llama al subworkflow 
Confirmar Presupuesto. Además, tiene una calculadora entre las tools para realizar los cálculos necesarios.

4. Como es un proyecto simple, ejecutado algunas veces por día por un único usuario, una Simple Memory es suficiente.

5. El chat model elegido fue GPT 4.1 mini.

6. Finaliza enviando el mensaje al usuario.


![subowrkflow precio]


Este es el subworkflow que contiene toda la base de datos necesaria para crear el presupuesto.
Es responsable de responder al Agente Principal sobre los tipos de muebles, variaciones, dimensiones, materiales, adicionales y precios.

Entonces, el usuario le envía un mensaje al bot indicando que quiere crear un nuevo presupuesto.
El bot responde pidiendo los datos necesarios (el mueble, las dimensiones, etc.).
El usuario responde, y el Agente Principal envía un único prompt de input al subworkflow con la información necesaria para conocer los precios y comenzar su trabajo.


![subworkflow registro]


Bien, entonces el usuario ya envió los datos, el Agente Principal verificó los precios con el subworkflow, hizo los cálculos y le envió al usuario el detalle completo del presupuesto por Telegram.

El siguiente paso es que el usuario compruebe que todo está correcto.
Después de esa revisión, el usuario dice “registrar presupuesto” y el Agente Principal llama al subworkflow RegistrodePresupuesto

1. El Agente Principal envía toda la información en un único prompt en formato string.

2. El node Code sirve para separar la información que llega como string y convertirla en datos organizados dentro de una tabla.
El motivo de este paso está explicado en  [02−Node por Node]

4. El node Aggregate vuelve a juntar los datos. El motivo también está explicado en  [02−Node por Node]

5. Un agente de IA cuya única función es registrar la información que estará presente en el documento PDF del presupuesto.


![subworkflow confirma]


Luego del registro del presupuesto, el usuario debe decir al bot “confirmar presupuesto”, y entonces el Agente Principal llama al subworkflow 
ConfirmaPresupuesto.

En este subworkflow no se utiliza ningún Agente de IA. Los detalles sobre la configuración de estos nodes están en [02−Node por Node]
Pero, para dar un panorama general, funciona así:

1. Los datos del presupuesto se extraen de la tabla momenta^neo y pasan por un node Code que separa cada detalle del presupuesto en distintos ítems.
Esto es muy importante para evitar errores cuando el presupuesto incluye dos o más muebles.

2. Después de que el node Code separa todos los ítems, el flujo continúa en Google Drive. Allí ya existe un documento template que sirve como base para todos los presupuestos.
El workflow hace una copia de ese template (esa copia será el documento específico del cliente). Luego, el node Update a Document completa esta copia con la información real del presupuesto, generando el archivo final en formato .docx.

3. Con el documento ya creado, falta convertirlo a PDF. El node Share File otorga permiso al node HTTP Request, que exporta el archivo en PDF y lo sube al Drive.

4. Con el documento final listo, el workflow envía un email al usuario mediante el node Send a message.

5. La tabla Momentaneo guarda solo los datos temporales necesarios para armar ese presupuesto. Esos datos no deben permanecer allí (el motivo se explica en 
[02−Node por Node]). Sin embargo, siguen siendo datos importantes para análisis futuros del negocio.
Por eso, antes de limpiar la tabla, un node Code imprime nuevamente toda la información y el flujo la envía a la tabla 
Historico donde queda almacenada de manera permanente. Luego de eso, el workflow borra la tabla Momentaneo
para dejarla lista para el próximo presupuesto.



