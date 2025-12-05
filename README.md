# Presupuesto-Automatico-N8N

Generación automática de presupuestos hecha en N8N; en este caso, fue desarrollada para una carpintería de Buenos Aires, pero puede adaptarse a distintos contextos.

Este repositorio no va a proporcionar el template en JSON del proyecto. Su propósito es funcionar tanto como documentación personal del proceso, como también ayudar a estudiantes de N8N que quieran mejorar de manera ética en la plataforma. Por lo tanto, acá vas a encontrar los problemas que fui encontrando en el camino, las soluciones y lo que pienso hacer diferente en proyectos similares en el futuro.

Si te interesó este proyecto, te quedó alguna duda o tenés alguna recomendación para que pueda mejorar y seguir evolucionando, por favor comunicate conmigo por email a: kaluanatuomate@gmail.com

# ¿Qué es?

Este es un workflow de generación automática de presupuestos hecho en N8N; en este caso, fue desarrollado para una carpintería de Buenos Aires, pero puede adaptarse a distintos contextos.

# ¿Qué problema resuelve?

En una breve conversación con el dueño de una carpintería de Buenos Aires, identificamos que perdían mucho tiempo en la creación y generación del documento de presupuesto que luego entregaban a sus clientes. Horas de la semana se iban en esta parte operativa, generando un gasto “invisible” para el negocio.

Con esta solución, todo se volvió más simple. El usuario (la persona responsable de crear el presupuesto) envía un mensaje por Telegram a un Bot (Agente de IA creado especialmente para este proyecto) diciendo “quiero crear un nuevo presupuesto”, y con una breve interacción con el bot, el presupuesto se genera y el documento en PDF queda listo. Todo se resuelve entre 3 y 5 minutos.4


# Requisitos previos

Para crear este workflow fue necesario:

N8N instalado

Creación de un bot en Telegram

Estructuración de la base de datos de la carpintería (Google Sheets)

APIs de Google Drive y Gmail

API de OpenAI para el chat model (GPT 4.1 mini) del Agente de IA

# Cómo está organizado el repositorio
/docs/

Documentación que explica cada parte del flujo

Incluye visión general, explicaciones node-por-node, errores y soluciones encontrados, etc.

Es donde está el contexto técnico del proyecto

/assets/

Imágenes utilizadas en la documentación
