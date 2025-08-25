# Calificacion de objetivos

# Estructura
1. LangChain: para ejecutar chunks de documentos y puede ejecutar los modelos de Ollama.
2. Ollama: ejecutar ollama de manera pura.
3. ApiGoogle: para usar el servicio de google con gemma.


### Prompt:
1. Opcion con SMART
```
Actúa como evaluador de objetivos. Recibirás el texto de un objetivo y debes calificar si está bien formulado según criterios SMART y de redacción. Limita tu salida exclusivamente a un JSON válido, sin texto adicional. Evalúa: 1) uso de un verbo en infinitivo ya sea al inicio o como principal (por ejemplo: “Aumentar”, “Reducir”, “Implementar”); 2) si responde a qué (qué se hará), para qué (propósito o impacto) y cómo (método o acciones); 3) SMART: medible (métricas o indicadores claros con números, porcentajes o umbrales), alcanzable (factible con recursos/plazo razonable), relevante (alineado al propósito y aporta valor) y con tiempo definido (fecha, plazo o ventana temporal concreta). Si el objetivo falla en cualquiera de estos puntos, marca “aprobado” como “NO” y explica qué falta o está mal, pero no seas muy estricto de calificar son objetivos de proyectos academicos de tesis de pregrado. Devuelve 3 sugerencias de posibles objetivos escritos correctamente; si todo está correcto, deja la lista de “opciones de sugerencias” vacía. En “verbos”, lista los verbos mal escritos o que no estén en infinitivo; si no hay problemas, devuelve una lista vacía. No inventes datos que no estén en el objetivo. Formato de salida obligatorio (JSON exacto): {"aprobado": "SI" | "NO", "verbos": ["..."], "detalle": "QUE ESTA MAL, QUE LE HACE FALTA EN CUMPLIMIENTO", "sugerencias": "QUE PUEDE MEJORAR SEMANTICAMENTE PARA SER APROBADO", "opciones de sugerencias": ["", "", ""]}. Objetivo a evaluar: """{PEGA_AQUI_TU_OBJETIVO}""". Notas: No incluyas nada fuera del JSON. Si el objetivo es ambiguo, explica brevemente en “detalle” qué ambigüedades impiden la evaluación y sugiere cómo precisarlo en “sugerencias”.
```


2. Opcion sin SMART
```
Actúa como evaluador de objetivos académicos de tesis de pregrado. Recibirás el texto de un objetivo y debes determinar si está correctamente formulado y redactado. Tu salida debe limitarse únicamente a un JSON válido, sin texto adicional fuera de él. Evalúa lo siguiente: 1) que el objetivo comience con un único verbo en infinitivo tomado de la taxonomía de Bloom (ejemplo: “Aumentar”, “Reducir”, “Implementar”); 2) que no exista más de un verbo en infinitivo; 3) que responda claramente a las preguntas: qué (acción principal), cómo (método o acciones) y para qué (propósito o impacto). Si alguno de estos criterios falla, marca “aprobado” como “NO” y explica en el campo “detalle” qué falta o qué está incorrecto. Considera además que estos objetivos pertenecen a proyectos académicos de carreras como producción, diseño u otras áreas afines, y que en ese contexto no es necesario dar respuesta a las tres preguntas planteadas.

Cuando el objetivo no cumpla, debes también generar 3 ejemplos alternativos de objetivos bien redactados, escritos en la forma adecuada. Si el objetivo cumple con todos los criterios, deja la lista de “opciones de sugerencias” vacía.

En el campo “verbos”, incluye cualquier verbo mal escrito o que no esté en infinitivo; si no hay problemas, devuélvelo como una lista vacía. No inventes datos que no estén en el objetivo.

El formato de salida debe ser exactamente este JSON:

{"aprobado": "SI" | "NO", "verbos": ["..."], "detalle": "QUE ESTA MAL, QUE LE HACE FALTA EN CUMPLIMIENTO", "sugerencias": "QUE PUEDE MEJORAR SEMÁNTICAMENTE PARA SER APROBADO", "opciones de sugerencias": ["", "", ""]}

Objetivo a evaluar: """PEGA_AQUI_TU_OBJETIVO"""

Notas finales: No incluyas nada fuera del JSON. Si el objetivo resulta ambiguo, explícitalo en el campo “detalle” y sugiere en “sugerencias” cómo reformularlo para mayor claridad.
```

### Ejemplo:
llama3.1
deepseek-r1:14b
gemma3:270m

```
Aumentar la competitividad de la empresa mejorando la Productividad y Calidad de sus operaciones, mediante la planeación, medición, análisis y mejora de sus procesos, teniendo como base fundamental el uso y la aplicación de modelos estadísticos. 

Aumentar el índice de productividad del departamento X en un 15% para diciembre de 2024, implementando un sistema de control basado en modelos estadísticos.

Reducir la tasa de defectos en el proceso Y a menos del 3% dentro de los próximos tres meses mediante análisis estadístico y aplicación de controles calidad.
```

```
Aumentar la satisfacción del cliente en un 15% para el tercer trimestre de 2025, implementando un nuevo sistema de soporte en línea y capacitando al equipo de atención al cliente.

Actúa como evaluador de objetivos. Recibirás el texto de un objetivo y debes calificar si está bien formulado según
criterios SMART y de redacción. Limita tu salida exclusivamente a un JSON válido, sin texto adicional. Evalúa: 1) us o de verbos en infinitivo al inicio (por ejemplo: “Aumentar”, “Reducir”, “Implementar”); 2) si responde a qué (qué se hará), para qué (propósito o impacto) y cómo (método o acciones); 3) SMART: medible (métricas o indicadores claros con números, porcentajes o umbrales), alcanzable (factible con recursos/plazo razonable), relevante (alineado al propósito y aporta valor) y con tiempo definido (fecha, plazo o ventana temporal concreta). Si el objetivo falla en cualquiera de estos puntos, marca “aprobado” como “NO” y explica qué falta o está mal, pero no seas muy estricto de calificar son objetivos de proyectos academicos de tesis de pregrado. Devuelve 3 sugerencias de posibles objetivos escritos correctamente; si todo está correcto, deja la lista de “opciones de sugerencias” vacía. En “verbos”, lista los verbos mal escritos o que no estén en infinitivo; si no hay problemas, devuelve una lista vacía. No inventes datos que no estén en el objetivo. Formato de salida obligatorio (JSON exacto): {"aprobado": "SI" | "NO", "verbos": ["..." ], "detalle": "QUE ESTA MAL, QUE LE HACE FALTA EN CUMPLIMIENTO", "sugerencias": "QUE PUEDE MEJORAR SEMANTICAMENTE PARA SER APROBADO", "opciones de sugerencias": ["", "", ""]}. Objetivo a evaluar: """Aumentar la satisfacción del cliente en un 15% para el tercer trimestre de 2025, implementando un nuevo sistema de soporte en línea y capacitando al equipo de atención al cliente.""". Notas: No incluyas nada fuera del JSON. Si el objetivo es ambiguo, explica brevemente en “detalle” qué ambigüedades impiden la evaluación y sugiere cómo precisarlo en “sugerencias”.



Respuestas:
{"aprobado": "SI", "verbos": [], "detalle": "", "sugerencias": "", "opciones de sugerencias": ["Aumentar un 15% la
satisfacción del cliente en el tercer trimestre de 2025, mediante implementación de nuevo sistema de soporte en
línea y capacitando al equipo de atención al cliente.", "Incrementar en 15% la satisfacción del cliente en el
tercer trimestre de 2025, desarrollando y aplicando un nuevo modelo de soporte en línea y entrenamiento para el
equipo de atención al cliente.", "Lograr una mejora del 15% en la satisfacción del cliente durante el tercer
trimestre de 2025, implementando un nuevo sistema de asistencia en línea y capacitación al equipo de atención al
cliente."]}


{\n  "aprobado": "NO",\n  "verbos": ["implementando", "capacitando"],\n  "detalle": "El objetivo cumple con la métrica de satisfacción del cliente (15%) pero no especifica cómo medirá el aumento ni si los métodos propuestos (\'implementar\' y \'capacitar\') son suficientes o cuáles serán las acciones exactas para lograrlo. Además, aunque tiene un plazo temporal (tercer trimestre de 2025), falta una explicación clara sobre la relación causal entre las acciones y el resultado medible.",\n  "sugerencias": "Especificar los indicadores clave de rendimiento (KPIs) exactos para medir la satisfacción del cliente, como encuestas específicas o métricas de servicio. Detallar cómo se realizará la capacitación y cuál será su impacto directo en las metas.",\n  "opciones de sugerencias": [\n    "Aumentar el puntaje promedio de satisfacción en encuestas post-interacción del cliente a un nivel específico (ej: >4/5) durante el tercer trimestre de 2025 mediante la implementación y uso constante del nuevo sistema de soporte.",\n    "Reducir el tiempo promedio de respuesta al correo electrónico de clientes con problemas, objetivo alcanzable para el tercer trimestre de 2025 después de implementar el chat en línea y capacitar al equipo en su manejo.",\n    "Implementar un programa piloto del nuevo sistema de soporte en línea durante el segundo semestre de 2024, evaluando una mejora específica en la satisfacción medible a través de análisis de datos."\n  ]\n}
```

```
Actúa como evaluador de objetivos. Recibirás el texto de un objetivo y debes calificar si está bien formulado según criterios SMART y de redacción. Limita tu salida exclusivamente a un JSON válido, sin texto adicional. Evalúa: 1) uso de verbos en infinitivo al inicio (por ejemplo: “Aumentar”, “Reducir”, “Implementar”); 2) si responde a qué (qué se hará), para qué (propósito o impacto) y cómo (método o acciones); 3) SMART: medible (métricas o indicadores claros con números, porcentajes o umbrales), alcanzable (factible con recursos/plazo razonable), relevante (alineado al propósito y aporta valor) y con tiempo definido (fecha, plazo o ventana temporal concreta). Si el objetivo falla en cualquiera de estos puntos, marca “aprobado” como “NO” y explica qué falta o está mal, pero no seas muy estricto de calificar son objetivos de proyectos academicos de tesis de pregrado. Devuelve 3 sugerencias de posibles objetivos escritos correctamente; si todo está correcto, deja la lista de “opciones de sugerencias” vacía. En “verbos”, lista los verbos mal escritos o que no estén en infinitivo; si no hay problemas, devuelve una lista vacía. No inventes datos que no estén en el objetivo. Formato de salida obligatorio (JSON exacto): {"aprobado": "SI" | "NO", "verbos": ["..."], "detalle": "QUE ESTA MAL, QUE LE HACE FALTA EN CUMPLIMIENTO", "sugerencias": "QUE PUEDE MEJORAR SEMANTICAMENTE PARA SER APROBADO", "opciones de sugerencias": ["", "", ""]}. Objetivo a evaluar: """Aumentar la competitividad de la empresa mejorando la Productividad y Calidad de sus operaciones, mediante la planeación, medición, análisis y mejora de sus procesos, teniendo como base fundamental el uso y la aplicación de modelos estadísticos""". Notas: No incluyas nada fuera del JSON. Si el objetivo es ambiguo, explica brevemente en “detalle” qué ambigüedades impiden la evaluación y sugiere cómo precisarlo en “sugerencias”.

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
```

2:11 a 2:15 pensando a 2:19
2:30 a 2:32 - 1:45 pensando a 2:34 - 1:50
2:38 para cargar comienza a escribir 

- 8 de ram para 7B de parametros
- 16 de ram para 13B de parametros
- 32 de ram para 33B de parametros
- 13 ram para 20B
