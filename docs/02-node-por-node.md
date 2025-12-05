# Workflow Principal


![workflow principal]


Como es obvio, el trigger es el mensaje que el usuario envía por Telegram. Telegram es un node nativo de n8n, entonces no hace falta instalar ningún community node.
Dependiendo de cómo tengas instalado tu n8n, no deberías tener problemas de funcionamiento; si los tenés, recomiendo mirar tutoriales en YouTube y revisar los accesos del firewall.


![edit field]

El Edit Field solo filtra los datos del Telegram que realmente importan: message y id.


![Agente Principal]

El Agente Principal usa el modelo GPT 4.1 mini. Como es un proyecto simple, ejecutado algunas veces por día por un único usuario interno, una Simple Memory es suficiente.

La tool Think sirve para ayudar al modelo a realizar cálculos Yo tenía problemas con el uso correcto de la tool Calculadora: el Agente no seguía órdenes lógicas y a veces devolvía resultados incorrectos.
La tool Think fue la mejor forma que encontré para reducir estos errores.

Las tres tools siguientes son los subworkflows. Como se explicó en [01−vision general], el Agente Principal no sabe nada: su única función es interactuar con el usuario y llamar a las tools correspondientes para obtener la información, registrar y confirmar.

El protocolo de comunicación entre los workflows está en [03−comu multi agents]

La estructura de los prompts está en [06−prompts].

El workflow finaliza con el node de enviar mensaje por Telegram.

# SUBWORKFLOW CONSULTA PRECIOS


![subworkflow precios]

El trigger aquí es “When executed by another workflow”, o sea, cuando el Agente Principal activa este subworkflow.


![trigger]


El Agente Consulta Precios tiene las tools necesarias para conocer toda la información para crear el presupuesto.
Cada tool es una sheet de Google que funciona como su base de datos, su cerebro.

Entonces, el Agente Principal lo activa pasándole los datos que el usuario proporcionó sobre el mueble a presupuestar.
El Consulta Precios verifica las tools y responde al Agente Principal.

# SUBWORKFLOW REGISTRO DE PRESUPUESTO


![subworkflow registro]


