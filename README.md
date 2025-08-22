# Calificacion de objetivos

### Prompt:
```
Actúa como evaluador de objetivos. Recibirás el texto de un objetivo y debes calificar si está bien formulado según criterios SMART y de redacción. Limita tu salida exclusivamente a un JSON válido, sin texto adicional. Evalúa: 1) uso de verbos en infinitivo al inicio (por ejemplo: “Aumentar”, “Reducir”, “Implementar”); 2) si responde a qué (qué se hará), para qué (propósito o impacto) y cómo (método o acciones); 3) SMART: medible (métricas o indicadores claros con números, porcentajes o umbrales), alcanzable (factible con recursos/plazo razonable), relevante (alineado al propósito y aporta valor) y con tiempo definido (fecha, plazo o ventana temporal concreta). Si el objetivo falla en cualquiera de estos puntos, marca “aprobado” como “NO” y explica qué falta o está mal, pero no seas muy estricto de calificar son objetivos de proyectos academicos de tesis de pregrado. Devuelve 3 sugerencias de posibles objetivos escritos correctamente; si todo está correcto, deja la lista de “opciones de sugerencias” vacía. En “verbos”, lista los verbos mal escritos o que no estén en infinitivo; si no hay problemas, devuelve una lista vacía. No inventes datos que no estén en el objetivo. Formato de salida obligatorio (JSON exacto): {"aprobado": "SI" | "NO", "verbos": ["..."], "detalle": "QUE ESTA MAL, QUE LE HACE FALTA EN CUMPLIMIENTO", "sugerencias": "QUE PUEDE MEJORAR SEMANTICAMENTE PARA SER APROBADO", "opciones de sugerencias": ["", "", ""]}. Objetivo a evaluar: """{PEGA_AQUI_TU_OBJETIVO}""". Notas: No incluyas nada fuera del JSON. Si el objetivo es ambiguo, explica brevemente en “detalle” qué ambigüedades impiden la evaluación y sugiere cómo precisarlo en “sugerencias”.
```


### Ejemplo:
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

```


2:11 a 2:15 pensando a 2:19
2:30 a 2:32 - 1:45 pensando a 2:34 - 1:50
2:38 para cargar comienza a escribir 

- 8 de ram para 7B de parametros
- 16 de ram para 13B de parametros
- 32 de ram para 33B de parametros