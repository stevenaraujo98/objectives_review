# Calificacion de objetivos

### Prompt:
```
Actúa como evaluador de objetivos. Recibirás el texto de un objetivo y debes calificar si está bien formulado según criterios SMART y de redacción. Limita tu salida exclusivamente a un JSON válido, sin texto adicional. Evalúa: 1) uso de verbos en infinitivo al inicio (por ejemplo: “Aumentar”, “Reducir”, “Implementar”); 2) si responde a qué (qué se hará), para qué (propósito o impacto) y cómo (método o acciones); 3) SMART: medible (métricas o indicadores claros con números, porcentajes o umbrales), alcanzable (factible con recursos/plazo razonable), relevante (alineado al propósito y aporta valor) y con tiempo definido (fecha, plazo o ventana temporal concreta). Si el objetivo falla en cualquiera de estos puntos, marca “aprobado” como “NO” y explica qué falta o está mal, pero no seas muy estricto de calificar son objetivos de proyectos academicos de tesis de pregrado. Devuelve 3 sugerencias de posibles objetivos escritos correctamente; si todo está correcto, deja la lista de “opciones de sugerencias” vacía. En “verbos”, lista los verbos mal escritos o que no estén en infinitivo; si no hay problemas, devuelve una lista vacía. No inventes datos que no estén en el objetivo. Formato de salida obligatorio (JSON exacto): {"aprobado": "SI" | "NO", "verbos": ["..."], "detalle": "QUE ESTA MAL, QUE LE HACE FALTA EN CUMPLIMIENTO", "sugerencias": "QUE PUEDE MEJORAR SEMANTICAMENTE PARA SER APROBADO", "opciones de sugerencias": ["", "", ""]}. Objetivo a evaluar: """{PEGA_AQUI_TU_OBJETIVO}""". Notas: No incluyas nada fuera del JSON. Si el objetivo es ambiguo, explica brevemente en “detalle” qué ambigüedades impiden la evaluación y sugiere cómo precisarlo en “sugerencias”.
```


### Ejemplo:
llama3.1
```
Aumentar la competitividad de la empresa mejorando la Productividad y Calidad de sus operaciones, mediante la planeación, medición, análisis y mejora de sus procesos, teniendo como base fundamental el uso y la aplicación de modelos estadísticos. 

Respuesta:



    "Aumentar el índice de productividad del departamento X en un 15% para diciembre de 2024,
implementando un sistema de control basado en modelos estadísticos.",
    "Reducir la tasa de defectos en el proceso Y a menos del 3% dentro de los próximos tres meses
mediante análisis estadístico y aplicación de controles calidad."
```

```
Aumentar la satisfacción del cliente en un 15% para el tercer trimestre de 2025, implementando un nuevo sistema de soporte en línea y capacitando al equipo de atención al cliente.

Respuesta:
Actúa como evaluador de objetivos. Recibirás el texto de un objetivo y debes calificar si está bien formulado según
... criterios SMART y de redacción. Limita tu salida exclusivamente a un JSON válido, sin texto adicional. Evalúa: 1) us
... o de verbos en infinitivo al inicio (por ejemplo: “Aumentar”, “Reducir”, “Implementar”); 2) si responde a qué (qué s
... e hará), para qué (propósito o impacto) y cómo (método o acciones); 3) SMART: medible (métricas o indicadores claros
...  con números, porcentajes o umbrales), alcanzable (factible con recursos/plazo razonable), relevante (alineado al pr
... opósito y aporta valor) y con tiempo definido (fecha, plazo o ventana temporal concreta). Si el objetivo falla en cu
... alquiera de estos puntos, marca “aprobado” como “NO” y explica qué falta o está mal, pero no seas muy estricto de ca
... lificar son objetivos de proyectos academicos de tesis de pregrado. Devuelve 3 sugerencias de posibles objetivos esc
... ritos correctamente; si todo está correcto, deja la lista de “opciones de sugerencias” vacía. En “verbos”, lista los
...  verbos mal escritos o que no estén en infinitivo; si no hay problemas, devuelve una lista vacía. No inventes datos
... que no estén en el objetivo. Formato de salida obligatorio (JSON exacto): {"aprobado": "SI" | "NO", "verbos": ["..."
... ], "detalle": "QUE ESTA MAL, QUE LE HACE FALTA EN CUMPLIMIENTO", "sugerencias": "QUE PUEDE MEJORAR SEMANTICAMENTE PA
... RA SER APROBADO", "opciones de sugerencias": ["", "", ""]}. Objetivo a evaluar: """Aumentar la satisfacción del clie
... nte en un 15% para el tercer trimestre de 2025, implementando un nuevo sistema de soporte en línea y capacitando al
... equipo de atención al cliente.""". Notas: No incluyas nada fuera del JSON. Si el objetivo es ambiguo, explica brevem
... ente en “detalle” qué ambigüedades impiden la evaluación y sugiere cómo precisarlo en “sugerencias”.
{"aprobado": "SI", "verbos": [], "detalle": "", "sugerencias": "", "opciones de sugerencias": ["Aumentar un 15% la
satisfacción del cliente en el tercer trimestre de 2025, mediante implementación de nuevo sistema de soporte en
línea y capacitando al equipo de atención al cliente.", "Incrementar en 15% la satisfacción del cliente en el
tercer trimestre de 2025, desarrollando y aplicando un nuevo modelo de soporte en línea y entrenamiento para el
equipo de atención al cliente.", "Lograr una mejora del 15% en la satisfacción del cliente durante el tercer
trimestre de 2025, implementando un nuevo sistema de asistencia en línea y capacitación al equipo de atención al
cliente."]}
```


Actúa como evaluador de objetivos. Recibirás el texto de un objetivo y debes calificar si está bien formulado según
... criterios SMART y de redacción. Limita tu salida exclusivamente a un JSON válido, sin texto adicional. Evalúa: 1) us
... o de verbos en infinitivo al inicio (por ejemplo: “Aumentar”, “Reducir”, “Implementar”); 2) si responde a qué (qué s
... e hará), para qué (propósito o impacto) y cómo (método o acciones); 3) SMART: medible (métricas o indicadores claros
...  con números, porcentajes o umbrales), alcanzable (factible con recursos/plazo razonable), relevante (alineado al pr
... opósito y aporta valor) y con tiempo definido (fecha, plazo o ventana temporal concreta). Si el objetivo falla en cu
... alquiera de estos puntos, marca “aprobado” como “NO” y explica qué falta o está mal, pero no seas muy estricto de ca
... lificar son objetivos de proyectos academicos de tesis de pregrado. Devuelve 3 sugerencias de posibles objetivos esc
... ritos correctamente; si todo está correcto, deja la lista de “opciones de sugerencias” vacía. En “verbos”, lista los
...  verbos mal escritos o que no estén en infinitivo; si no hay problemas, devuelve una lista vacía. No inventes datos
... que no estén en el objetivo. Formato de salida obligatorio (JSON exacto): {"aprobado": "SI" | "NO", "verbos": ["..."
... ], "detalle": "QUE ESTA MAL, QUE LE HACE FALTA EN CUMPLIMIENTO", "sugerencias": "QUE PUEDE MEJORAR SEMANTICAMENTE PA
... RA SER APROBADO", "opciones de sugerencias": ["", "", ""]}. Objetivo a evaluar: """Aumentar la competitividad de la
... empresa mejorando la Productividad y Calidad de sus operaciones, mediante la planeación, medición, análisis y mejora
...  de sus procesos, teniendo como base fundamental el uso y la aplicación de modelos estadísticos""". Notas: No incluy
... as nada fuera del JSON. Si el objetivo es ambiguo, explica brevemente en “detalle” qué ambigüedades impiden la evalu
... ación y sugiere cómo precisarlo en “sugerencias”.
{"aprobado": "NO", "verbos": ["mejorando"], "detalle": "No se define claramente con qué recursos o plazo factible
se cuenta para lograr el objetivo. No existe indicador claro de medición del aumento en la competitividad.",
"sugerencias": "Establecer una métrica específica y medible para evaluar el éxito del aumento en competitividad.
Definir un plan detallado con recursos, plazo y responsables para la implementación. Especificar claramente qué
modelos estadísticos se utilizarán.", "opciones de sugerencias": ["Aumentar la competitividad de la empresa en un
15% mejorando la Productividad y Calidad de sus operaciones, mediante la planeación, medición, análisis y mejora
de sus procesos, teniendo como base fundamental el uso y la aplicación de modelos estadísticos", "Incrementar
significativamente la competitividad de la empresa mejorando la Productividad y Calidad de las operaciones en un
20% dentro del primer año, mediante estrategias centradas en la planeación, medición, análisis y mejora continua
de procesos utilizando herramientas estadísticas.", "Mejorar sustancialmente la competitividad de la empresa
aumentando en un 15% la Productividad y Calidad de las operaciones dentro de los próximos 18 meses mediante
estrategias basadas en el uso y aplicación efectiva de modelos estadísticos para la planeación, medición, análisis
y mejora continua."] }


2:11 a 2:15 pensando a 2:19
2:30 a 2:32 - 1:45 pensando a 2:34 - 1:50
2:38 para cargar comienza a escribir 

- 8 de ram para 7B de parametros
- 16 de ram para 13B de parametros
- 32 de ram para 33B de parametros