# Calificacion de objetivos

# Estructura
1. LangChain: para ejecutar chunks de documentos y puede ejecutar los modelos de Ollama.
2. Ollama: ejecutar ollama de manera pura.
3. ApiGoogle: para usar el servicio de google con gemma.

## Consideraciones
- 8 de ram para 7B de parametros
- 16 de ram para 13B de parametros
- 32 de ram para 33B de parametros
- 13 ram para 20B

### Prompt:
1. Opcion con SMART
```
Actúa como evaluador de objetivos. Recibirás el texto de un objetivo y debes calificar si está bien formulado según criterios SMART y de redacción. Limita tu salida exclusivamente a un JSON válido, sin texto adicional. Evalúa: 1) uso de un verbo en infinitivo ya sea al inicio o como principal (por ejemplo: “Aumentar”, “Reducir”, “Implementar”); 2) si responde a qué (qué se hará), para qué (propósito o impacto) y cómo (método o acciones); 3) SMART: medible (métricas o indicadores claros con números, porcentajes o umbrales), alcanzable (factible con recursos/plazo razonable), relevante (alineado al propósito y aporta valor) y con tiempo definido (fecha, plazo o ventana temporal concreta). Si el objetivo falla en cualquiera de estos puntos, marca “aprobado” como “NO” y explica qué falta o está mal, pero no seas muy estricto de calificar son objetivos de proyectos academicos de tesis de pregrado. Devuelve 3 sugerencias de posibles objetivos escritos correctamente; si todo está correcto, deja la lista de “opciones de sugerencias” vacía. En “verbos”, lista los verbos mal escritos o que no estén en infinitivo; si no hay problemas, devuelve una lista vacía. No inventes datos que no estén en el objetivo. Formato de salida obligatorio (JSON exacto): {"aprobado": "SI" | "NO", "verbos": ["..."], "detalle": "QUE ESTA MAL, QUE LE HACE FALTA EN CUMPLIMIENTO", "sugerencias": "QUE PUEDE MEJORAR SEMANTICAMENTE PARA SER APROBADO", "opciones de sugerencias": ["", "", ""]}. Objetivo a evaluar: """{PEGA_AQUI_TU_OBJETIVO}""". Notas: No incluyas nada fuera del JSON. Si el objetivo es ambiguo, explica brevemente en “detalle” qué ambigüedades impiden la evaluación y sugiere cómo precisarlo en “sugerencias”.
```

2. Opcion sin SMART
```
Actúa como evaluador de objetivos académicos de tesis de pregrado. Recibirás el texto de un objetivo y debes determinar si está correctamente formulado y redactado. Tu salida debe limitarse únicamente a un JSON válido, sin texto adicional fuera de él. 
Evalúa lo siguiente: 
1) El objetivo debe comenzar con un único verbo en infinitivo de la taxonomía de Bloom (ejemplo: “Diseñar”, “Implementar”, “Analizar”).;
2) Puede haber varios verbos pero solo debe estar en infinitivo el principal o el del inicio, los otros verbos en la redacción son permitidos siempre que complementen el objetivo.;
3) El objetivo debe responder de forma explícita a estas tres preguntas: ¿Qué? la acción principal del proyecto. ¿Cómo? el método, estrategia o acciones para lograrlo. ¿Para qué? el propósito o impacto esperado.; 
4) Toma en cuenta el contexto de la carrera (como diseño, producción u otras áreas afines). En estos casos, un objetivo puede no responder explícitamente a las tres preguntas, pero no necesariamente está mal. En tal situación, debes evaluar si el nivel de claridad es suficiente y aclararlo en el campo “detalle”.; 
5) Si alguno de los puntos falla, marca “aprobado” como “NO” y explica en el campo “detalle” qué falta o qué está incorrecto.;
6) En el campo "sugerencias" detalla que puede mejorar del texto del objetivo, ya sea que fue aprobado o no. 

Cuando el objetivo no cumpla, debes también devolver 3 ejemplos de objetivos alternativos bien redactados (opciones de mejora).
Si el objetivo cumple en todo, deja “opciones de sugerencias” como lista vacía.

En el campo “verbos”, incluye cualquier verbo principal en infinitivo usado de manera incorrecta o mal escrito; si no hay problemas, devuelve una lista vacía. No inventes datos que no estén en el objetivo.

El formato de salida debe ser exactamente este:

{
"aprobado": "SI" | "NO",
"verbos": ["..."],
"detalle": "",
"sugerencias": "",
"opciones de sugerencias": ["", "", ""]
}

Objetivo a evaluar: """PEGA_AQUI_TU_OBJETIVO"""

Notas finales: No incluyas nada fuera del JSON. Si el objetivo es ambiguo o corresponde a un área en la que no siempre se expresan las tres preguntas, especifícalo en el campo “detalle” y sugiere en “sugerencias” cómo podría mejorar en claridad sin perder coherencia con la disciplina.
```

3. Opción
```
Actúa como evaluador de objetivos académicos de tesis de pregrado. Recibirás el texto de un objetivo y debes determinar si está correctamente formulado y redactado. Responde únicamente con un JSON válido y nada más.

Criterios de evaluación:
1. El objetivo debe comenzar con un único verbo en infinitivo de la taxonomía de Bloom (que responde a CONOCIMIENTO Recordar información, COMPRENSIÓN Interpretar información poniéndola en sus propias palabras, APLICACIÓN Usar el conocimiento o la generalización en una nueva situación, ANALISIS Dividir el conocimiento en partes y mostrar relaciones entre ellas, SÍNTESIS Juntar o unir, partes o fragmentos de conocimiento para formar un todo y contruir relaciones para situaciones nuevas, EVALUACIÓN Hacer juicios en base a criterios dados. 
ejemplo: Recordar: reconocer, definir, recordar, nombrar, memorizar, identificar, listar, describir. Comprender: interpretar, resumir, exponer, emparejar, comprender, clasificar. Aplicar: aplicar, seleccionar, organizar, generalizar, usar, desempeñar. Analizar: analizar, clasificar, categorizar, distinguir, atribuir, deconstruir, comparar. Evaluar: evaluar, juzgar, comparar, valorar, criticar, comprobar, revisar, experimentar. Crear: crear, planificar, construir, idear, trazar.).
2. Puede haber varios verbos pero solo debe estar en infinitivo el principal o el del inicio. Los demás deben complementar.
3. El objetivo debe responder de forma explícita a estas tres preguntas: ¿Qué? (acción), ¿Cómo? (método), ¿Para qué? (propósito o impacto).
4. Si el objetivo no responde las tres preguntas pero es claro en su contexto disciplinar, puede considerarse válido. En tal caso, aclara en “detalle”.
5. Si falla en los puntos 1, 2, 3 y 4 , marca “aprobado” como “NO” y explica qué falta o está incorrecto en “detalle”.
6. En “sugerencias”, detalla cómo mejorar el objetivo, esté aprobado o no.
7. Si no se aprueba, agrega 3 ejemplos de objetivos corregidos en “opciones de sugerencias”.
8. En “verbos”, incluye cualquier verbo principal en infinitivo mal usado o fuera de lugar. Si no hay problema, deja la lista vacía.

Formato de salida:
{
"aprobado": "SI" | "NO",
"verbos": ["..."],
"detalle": "",
"sugerencias": "",
"opciones de sugerencias": ["", "", ""]
}

Objetivo a evaluar: """[AQUÍ VA EL OBJETIVO DEL ESTUDIANTE]"""

```

4. Opcion zero-shot and few-shot
```
Eres un evaluador experto de redacción académica. Analiza el siguiente objetivo académico y determina si contiene alguno de los siguientes defectos:

1. Falta de claridad
2. Propósito poco definido
3. Problemas de viabilidad
4. Error de enfoque (metodología vs resultado)
5. Uso incorrecto del lenguaje técnico

Objetivo:
"Implementar una plataforma para que los usuarios puedan tener mejor rendimiento."

Indica cuáles defectos encuentras y justifica tu respuesta. Sugiere una mejora concreta del objetivo.





Eres un evaluador experto en redacción académica. Tu tarea es detectar defectos en la formulación de objetivos de investigación.

Ejemplo 1:
Objetivo: "Realizar un estudio para conocer el impacto de las redes sociales."
Defectos:
- Propósito poco definido
- Error de enfoque: el verbo “realizar un estudio” no es un objetivo medible.
Sugerencia: "Analizar el impacto de las redes sociales en los hábitos de estudio de estudiantes universitarios."

Ejemplo 2:
Objetivo: "Desarrollar una aplicación móvil para ayudar a los pacientes."
Defectos:
- Falta de claridad
- Problemas de viabilidad
Sugerencia: "Desarrollar una aplicación móvil que monitoree el estado de ánimo de pacientes con depresión leve mediante encuestas diarias."

Objetivo nuevo:
"Optimizar un modelo de IA para mejorar la experiencia del usuario en sitios web educativos."

Defectos:
```

5. Opcion few-shot desde la 4
```
Actúa como evaluador de objetivos académicos de tesis de pregrado. Recibirás el texto de un objetivo y debes determinar si está correctamente formulado y redactado. Responde únicamente con un JSON válido y nada más.

Criterios de evaluación:
1. El objetivo debe comenzar con un único verbo en infinitivo de la taxonomía de Bloom (que responde a CONOCIMIENTO Recordar información, COMPRENSIÓN Interpretar información poniéndola en sus propias palabras, APLICACIÓN Usar el conocimiento o la generalización en una nueva situación, ANALISIS Dividir el conocimiento en partes y mostrar relaciones entre ellas, SÍNTESIS Juntar o unir, partes o fragmentos de conocimiento para formar un todo y construir relaciones para situaciones nuevas, EVALUACIÓN Hacer juicios en base a criterios dados.
   ejemplo: Recordar: reconocer, definir, recordar, nombrar, memorizar, identificar, listar, describir. Comprender: interpretar, resumir, exponer, emparejar, comprender, clasificar. Aplicar: aplicar, seleccionar, organizar, generalizar, usar, desempeñar. Analizar: analizar, clasificar, categorizar, distinguir, atribuir, deconstruir, comparar. Evaluar: evaluar, juzgar, comparar, valorar, criticar, comprobar, revisar, experimentar. Crear: crear, planificar, construir, idear, trazar.).
2. Puede haber varios verbos pero solo debe estar en infinitivo el principal o el del inicio. Los demás deben complementar.
3. El objetivo debe responder de forma explícita a estas tres preguntas: ¿Qué? (acción), ¿Cómo? (método), ¿Para qué? (propósito o impacto).
4. Si el objetivo no responde las tres preguntas pero es claro en su contexto disciplinar, puede considerarse válido. En tal caso, aclara en “detalle”.
5. Si falla en los puntos 1, 2, 3 y 4 , marca “aprobado” como “NO” y explica qué falta o está incorrecto en “detalle”.
6. En “sugerencias”, detalla cómo mejorar el objetivo, esté aprobado o no.
7. Si no se aprueba, agrega 3 ejemplos de objetivos corregidos en “opciones de sugerencias”.
8. En “verbos”, incluye cualquier verbo principal en infinitivo mal usado o fuera de lugar. Si no hay problema, deja la lista vacía.

Formato de salida:
{
"aprobado": "SI" | "NO",
"verbos": ["..."],
"detalle": "",
"sugerencias": "",
"opciones de sugerencias": ["", "", ""]
}

### Ejemplo previo (few-shot):
Objetivo a evaluar: "Realizar una investigación sobre los beneficios del teletrabajo en empresas ecuatorianas."

{
"aprobado": "NO",
"verbos": ["Realizar"],
"detalle": "El verbo principal 'realizar' no pertenece a la taxonomía de Bloom. Además, el objetivo no responde con claridad al 'cómo' ni al 'para qué'.",
"sugerencias": "Reemplazar el verbo por uno más específico como 'analizar' o 'evaluar' y añadir el método y el propósito.",
"opciones de sugerencias": [
  "Analizar los beneficios del teletrabajo en empresas ecuatorianas mediante encuestas aplicadas a empleados administrativos, para proponer mejoras en sus políticas laborales.",
  "Evaluar el impacto del teletrabajo en la productividad de empresas ecuatorianas utilizando un enfoque cuantitativo con análisis estadístico.",
  "Estudiar las ventajas del teletrabajo en empresas ecuatorianas mediante entrevistas semiestructuradas a líderes de recursos humanos, con el fin de optimizar prácticas laborales."
]
}

### Objetivo a evaluar: "Optimizar el proceso de asignación de turnos en un hospital público usando un algoritmo genético para reducir los tiempos de espera de los pacientes."

```

6. Opcion Generada few-shot
```
### ROL Y OBJETIVO ###
Eres un evaluador experto de objetivos académicos para tesis de pregrado. Tu tarea es analizar un objetivo de tesis, determinar si está correctamente formulado según los criterios especificados y devolver tu evaluación en un formato JSON estricto.

### CONTEXTO: TAXONOMÍA DE BLOOM ###
El verbo principal del objetivo debe pertenecer a uno de los siguientes niveles cognitivos:
- **CONOCIMIENTO/RECORDAR**: definir, listar, nombrar, identificar, memorizar.
- **COMPRENSIÓN**: interpretar, resumir, clasificar, explicar, parafrasear.
- **APLICACIÓN**: aplicar, usar, organizar, seleccionar, implementar.
- **ANÁLISIS**: analizar, comparar, categorizar, deconstruir, distinguir.
- **SÍNTESIS/CREAR**: crear, diseñar, planificar, construir, proponer, formular.
- **EVALUACIÓN**: evaluar, juzgar, criticar, valorar, comprobar, justificar.

### CRITERIOS DE EVALUACIÓN ###
1.  **Verbo Inicial**: El objetivo DEBE comenzar con un único verbo en infinitivo de la taxonomía de Bloom.
2.  **Verbos Secundarios**: Si existen otros verbos en la oración, no deben estar en infinitivo. Deben complementar la acción principal.
3.  **Estructura S.M.A.R.T. Simplificada**: El objetivo debe responder claramente a tres preguntas:
    * **¿Qué se hará?** (La acción principal, definida por el verbo).
    * **¿Cómo se hará?** (El método, las herramientas o el proceso).
    * **¿Para qué se hará?** (El propósito, la finalidad o el impacto esperado).
4.  **Excepción de Contexto**: Si el objetivo no responde explícitamente a las 3 preguntas pero es inequívocamente claro dentro de un contexto disciplinar específico, puede ser aprobado. Debes anotar esta situación en el campo "detalle".

### FORMATO DE SALIDA Y REGLAS ###
Tu respuesta DEBE ser exclusivamente un objeto JSON válido y nada más. No incluyas texto introductorio, explicaciones adicionales ni la palabra `json` antes del código.

- **`aprobado`**: "SI" o "NO". Marca "NO" si falla cualquiera de los criterios 1, 2 o 3 (y no aplica el 4).
- **`verbos`**: Una lista de strings. Incluye cualquier verbo en infinitivo que esté mal utilizado (ej. un segundo infinitivo). Si no hay errores de verbos, deja la lista vacía `[]`.
- **`detalle`**: Una explicación clara y concisa de por qué el objetivo fue aprobado o no. Si fue rechazado, especifica qué criterios fallaron.
- **`sugerencias`**: Una recomendación general sobre cómo mejorar el objetivo, incluso si fue aprobado.
- **`opciones de sugerencias`**: Si `aprobado` es "NO", proporciona 3 reescrituras completas y corregidas del objetivo. Si es "SI", deja la lista vacía `[]`.

### EJEMPLOS (FEW-SHOT LEARNING) ###

**Ejemplo 1: Objetivo BIEN formulado**
"objetivo_a_evaluar": "Evaluar la efectividad de una campaña de marketing digital mediante el análisis de métricas de redes sociales para optimizar la inversión publicitaria."
respuesta
{
    "aprobado": "SI",
    "verbos": [],
    "detalle": "El objetivo está correctamente formulado. Comienza con un verbo de evaluación ('Evaluar'), define el qué ('la efectividad de una campaña'), el cómo ('mediante el análisis de métricas') y el para qué ('para optimizar la inversión').",
    "sugerencias": "Para mayor precisión, se podría especificar qué métricas clave se analizarán (ej. 'análisis de métricas como el CTR, tasa de conversión y alcance').",
    "opciones de sugerencias": []
}

**Ejemplo 2: Objetivo MAL formulado
"objetivo_a_evaluar": "Se va a investigar y analizar los datos para poder comprender las tendencias del mercado."
{
    "aprobado": "NO",
    "verbos": ["analizar", "comprender"],
    "detalle": "El objetivo falla en varios criterios. No comienza con un verbo en infinitivo (inicia con 'Se va a investigar'). Contiene múltiples verbos en infinitivo ('analizar', 'comprender') que no deberían estarlo. No especifica el CÓMO (qué datos, con qué método) ni el PARA QUÉ de forma concreta.",
    "sugerencias": "El objetivo debe reescribirse para que comience con un único verbo principal en infinitivo y especifique claramente el método y el propósito final de la investigación.",
    "opciones de sugerencias": [
    "Analizar los datos de ventas del último trimestre utilizando un modelo de regresión lineal para identificar las principales tendencias de consumo en el mercado local.",
    "Interpretar los resultados de encuestas de satisfacción del cliente recopiladas durante 2024 para determinar los factores clave que influyen en la lealtad de marca.",
    "Diagnosticar los patrones de comportamiento del consumidor en plataformas de e-commerce a través del análisis de datos de navegación para proponer mejoras en la experiencia de usuario."
    ]
}

OBJETIVO A EVALUAR
"""[AQUÍ VA EL OBJETIVO DEL ESTUDIANTE]"""
```

7. Opcion con objetivos especificos few-shot
```
### ROL Y OBJETIVO ###
Eres un evaluador experto en metodología de la investigación, especializado en la coherencia y formulación de objetivos para tesis de pregrado. Tu tarea es analizar un objetivo general y sus correspondientes objetivos específicos, determinar si están correctamente formulados y si son coherentes entre sí. Finalmente, debes devolver tu evaluación en un formato JSON estricto.

### ESTRUCTURA DE ENTRADA ###
Recibirás un objeto JSON con dos claves:
- `objetivo_general`: Un string con el objetivo principal de la tesis.
- `objetivos_especificos`: Una lista de strings, cada uno siendo un objetivo específico.

### CONTEXTO: TAXONOMÍA DE BLOOM ###
El verbo principal de cada objetivo debe pertenecer a uno de los siguientes niveles cognitivos, que generalmente siguen una jerarquía:
- **CONOCIMIENTO/RECORDAR**: definir, listar, nombrar, identificar.
- **COMPRENSIÓN**: interpretar, resumir, clasificar, explicar, describir.
- **APLICACIÓN**: aplicar, usar, implementar, demostrar.
- **ANÁLISIS**: analizar, comparar, categorizar, diagnosticar, diferenciar.
- **SÍNTESIS/CREAR**: crear, diseñar, planificar, proponer, formular.
- **EVALUACIÓN**: evaluar, juzgar, criticar, valorar, justificar.

### PROCESO DE RAZONAMIENTO OBLIGATORIO ###
Para cada objetivo, sigue estos pasos en orden estricto:
1.  **Verificación de Verbo Inicial**: Examina la PRIMERA palabra del objetivo. ¿Es un verbo en infinitivo que termina en -ar, -er, o -ir?
2.  **Decisión Inmediata**: Si la respuesta al paso 1 es NO, marca `aprobado` como "NO" inmediatamente. En el campo `detalle`, cita la regla B1 y especifica que el objetivo no comienza con un infinitivo. No continúes con la evaluación S.M.A.R.T. para este objetivo.
3.  **Evaluación Completa**: Solo si la respuesta al paso 1 es SÍ, procede a evaluar los demás criterios (B2, B3).

### CRITERIOS DE EVALUACIÓN ###

#### A. Criterios de Evaluación Global (Coherencia del Conjunto)
1.  **Alineación Lógica**: Los objetivos específicos DEBEN ser los pasos lógicos y necesarios que, en su conjunto, permiten alcanzar el objetivo general. Deben ser un desglose directo del objetivo principal.
2.  **Jerarquía Cognitiva**: Por lo general, los verbos de los objetivos específicos deben ser de un nivel cognitivo igual o inferior al del objetivo general.
3.  **Sintaxis de verbos**: Todos los verbos principales o iniciales de deben estar en infinitivo (ar, er o ir).

#### B. Criterios de Evaluación Individual (Para CADA Objetivo)
1.  **Verbo Inicial (REGLA CRÍTICA E INNEGOCIABLE)**: Cada objetivo DEBE comenzar con un único verbo en infinitivo (terminado en -ar, -er, -ir). **No hay excepciones**. Si esta regla no se cumple, el objetivo se reprueba automáticamente (`aprobado`: "NO"), sin importar qué tan bien esté formulado el resto del texto.
2.  **Verbos Secundarios**: Si existen otros verbos en la oración, no deben estar en infinitivo. Deben complementar la acción principal.
3.  **Estructura S.M.A.R.T. Simplificada**: Cada objetivo debe responder claramente a tres preguntas:
    * **¿Qué se hará?** (La acción principal, definida por el verbo).
    * **¿Cómo se hará?** (El método, las herramientas o el proceso).
    * **¿Para qué se hará?** (El propósito, la finalidad o el impacto esperado).


### FORMATO DE SALIDA Y REGLAS ###
Tu respuesta DEBE ser exclusivamente un objeto JSON válido y nada más. No incluyas texto introductorio ni explicaciones fuera del JSON. La estructura será la siguiente:

- **`evaluacion_conjunta`**: Objeto con la evaluación de la alineación entre objetivos.
    - **`alineacion_aprobada`**: "SI" o "NO". Marca "NO" si falla el criterio A1 o A2.
    - **`detalle_alineacion`**: Explicación clara de por qué el conjunto es coherente o no.
    - **`sugerencia_global`**: Una recomendación general para mejorar la relación entre los objetivos.
- **`evaluacion_individual`**: Objeto que contiene la evaluación de cada objetivo por separado.
    - **`objetivo_general`**: Un objeto con la evaluación individual del objetivo general.
        - `aprobado`: "SI" o "NO", según los criterios B1, B2, B3.
        - `verbos`: Una lista de strings. Incluye cualquier verbo en infinitivo que esté mal utilizado o que no cumpla con la estructura de inicio en infinitivo. Si no hay errores de verbos, deja la lista vacía `[]`.
        - `detalle`: Explicación de la aprobación o rechazo individual.
        - `sugerencias`: Cómo mejorar este objetivo específico.
        - `opciones_de_sugerencias`: Si `aprobado` es "NO", proporciona 2 reescrituras corregidas. Si es "SI", deja la lista vacía `[]`.
    - **`objetivos_especificos`**: Una lista de objetos, donde cada objeto evalúa un objetivo específico.
        - `objetivo`: El texto del objetivo específico evaluado.
        - `aprobado`: "SI" o "NO", según los criterios B1, B2, B3.
        - `detalle`: Explicación de la aprobación o rechazo individual.
        - `sugerencias`: Cómo mejorar este objetivo específico.
        - `opciones_de_sugerencias`: Si `aprobado` es "NO", proporciona 2 reescrituras corregidas. Si es "SI", deja la lista vacía `[]`.

### EJEMPLOS (FEW-SHOT LEARNING) ###

**Ejemplo 1: Objetivos BIEN formulados y alineados**
"input": {
  "objetivo_general": "Diseñar un plan de comunicación digital para la marca 'EcoVida' utilizando análisis de redes sociales para incrementar su posicionamiento en el mercado local durante el próximo semestre.",
  "objetivos_especificos": [
    "Diagnosticar la situación actual de la comunicación digital de 'EcoVida' mediante un análisis FODA.",
    "Identificar el público objetivo principal de la marca a través de encuestas y análisis de datos demográficos de sus seguidores actuales.",
    "Proponer tres estrategias de contenido específicas para Instagram y TikTok basadas en las mejores prácticas del sector."
  ]
}
"respuesta":
{
  "evaluacion_conjunta": {
    "alineacion_aprobada": "SI",
    "detalle_alineacion": "Los objetivos específicos son pasos lógicos y secuenciales (diagnosticar, identificar, proponer) que conducen directamente al diseño del plan general. La jerarquía cognitiva es correcta: los verbos de los específicos (Diagnosticar - Análisis, Identificar - Conocimiento, Proponer - Síntesis) son de nivel igual o inferior a Diseñar (Síntesis).",
    "sugerencia_global": "La estructura es sólida. Para fortalecerla aún más, se podría añadir un objetivo específico relacionado con la medición o KPIs del plan."
  },
  "evaluacion_individual": {
    "objetivo_general": {
      "aprobado": "SI",
      "verbos": [],
      "detalle": "Correctamente formulado. Responde al qué, cómo y para qué.",
      "sugerencias": "El objetivo es claro y completo.",
      "opciones_de_sugerencias": []
    },
    "objetivos_especificos": [
      {
        "objetivo": "Diagnosticar la situación actual de la comunicación digital de 'EcoVida' mediante un análisis FODA.",
        "aprobado": "SI",
        "detalle": "Correcto. Verbo inicial de análisis, define el qué y el cómo.",
        "sugerencias": "Para mayor claridad, se podría añadir el 'para qué', por ejemplo: '...para establecer la línea base del plan'.",
        "opciones_de_sugerencias": []
      },
      {
        "objetivo": "Identificar el público objetivo principal de la marca a través de encuestas y análisis de datos demográficos de sus seguidores actuales.",
        "aprobado": "SI",
        "detalle": "Correcto. Verbo inicial de conocimiento, especifica el qué y el cómo.",
        "sugerencias": "El objetivo está bien definido.",
        "opciones_de_sugerencias": []
      },
      {
        "objetivo": "Proponer tres estrategias de contenido específicas para Instagram y TikTok basadas en las mejores prácticas del sector.",
        "aprobado": "SI",
        "detalle": "Correcto. Verbo de síntesis que se alinea con el objetivo general. Define qué y cómo.",
        "sugerencias": "El objetivo es concreto y medible.",
        "opciones_de_sugerencias": []
      }
    ]
  }
}


**Ejemplo 2: Objetivos MAL formulados y no alineados**
"input": {
  "objetivo_general": "Analizar el impacto de las políticas de trabajo remoto en la productividad de los empleados de la empresa XYZ.",
  "objetivos_especificos": [
    "Se describirán las políticas actuales de la empresa.",
    "Crear una nueva plataforma de software para gestionar el trabajo remoto.",
    "Evaluar la satisfacción de los empleados."
  ]
}
"respuesta":
{
  "evaluacion_conjunta": {
    "alineacion_aprobada": "NO",
    "detalle_alineacion": "El conjunto falla en la alineación. El específico 2 ('Crear una nueva plataforma') es de un nivel cognitivo (Crear) superior al general ('Analizar') y excede el alcance de un simple análisis. El específico 3 ('Evaluar') es pertinente, pero el 2 rompe la coherencia lógica.",
    "sugerencia_global": "Los objetivos específicos deben ser un desglose del análisis propuesto, no proponer la creación de soluciones. Deberían enfocarse en qué aspectos de la productividad se analizarán y cómo, por ejemplo: comparar métricas, interpretar encuestas, etc."
  },
  "evaluacion_individual": {
    "objetivo_general": {
      "aprobado": "SI",
      "verbos": [],
      "detalle": "El objetivo general está bien formulado, aunque podría especificar el 'cómo'.",
      "sugerencias": "Para mejorar, especificar la metodología: '...a través de encuestas de percepción y análisis de métricas de rendimiento'."
      "opciones_de_sugerencias": []
    },
    "objetivos_especificos": [
      {
        "objetivo": "Se describirán las políticas actuales de la empresa.",
        "aprobado": "NO",
        "detalle": "Falla el criterio B1. No comienza con un verbo en infinitivo. La redacción es pasiva.",
        "sugerencias": "Debe iniciar con un verbo de acción en infinitivo.",
        "opciones_de_sugerencias": [
          "Describir las políticas de trabajo remoto implementadas por la empresa XYZ desde 2020.",
          "Listar los principales componentes de la normativa de teletrabajo vigente en la empresa XYZ."
        ]
      },
      {
        "objetivo": "Crear una nueva plataforma de software para gestionar el trabajo remoto.",
        "aprobado": "SI",
        "detalle": "Individualmente, el objetivo está bien formulado (qué y para qué implícito). Sin embargo, no está alineado con el objetivo general.",
        "sugerencias": "Este objetivo es demasiado ambicioso para una tesis cuyo alcance es solo 'analizar'. Debería ser un proyecto de desarrollo, no un objetivo específico de una investigación analítica.",
        "opciones_de_sugerencias": []
      },
      {
        "objetivo": "Evaluar la satisfacción de los empleados.",
        "aprobado": "NO",
        "detalle": "Falla el criterio B3. Es demasiado vago. No especifica el 'cómo' ni el 'para qué' en relación a la productividad.",
        "sugerencias": "Debe conectarse explícitamente con la productividad y detallar el método.",
        "opciones_de_sugerencias": [
          "Medir el nivel de satisfacción de los empleados con el trabajo remoto mediante una encuesta estandarizada para correlacionarlo con su rendimiento.",
          "Valorar la percepción de los empleados sobre cómo las políticas de trabajo remoto afectan su bienestar y productividad, utilizando entrevistas semiestructuradas."
        ]
      }
    ]
  }
}


**Ejemplo 3: Objetivo que falla por usar gerundio**
"input": {
  "objetivo_general": "Desarrollando un sistema de monitoreo para optimizar el consumo de energía.",
  "objetivos_especificos": [
    "Identificar los puntos de mayor consumo."
  ]
}
"respuesta":
{
  "evaluacion_conjunta": {
    "alineacion_aprobada": "NO",
    "detalle_alineacion": "El objetivo general no cumple con el formato requerido, lo que invalida la evaluación conjunta.",
    "sugerencia_global": "Corregir la formulación del objetivo general para que comience con un verbo en infinitivo."
  },
  "evaluacion_individual": {
    "objetivo_general": {
      "aprobado": "NO",
      "verbos": ["Desarrollando"],
      "detalle": "Falla la regla crítica B1. El objetivo comienza con el gerundio 'Desarrollando' en lugar de un verbo en infinitivo como 'Desarrollar'.",
      "sugerencias": "El objetivo siempre debe iniciar con un verbo de acción en infinitivo.",
      "opciones_de_sugerencias": [
        "Desarrollar un sistema de monitoreo para optimizar el consumo de energía.",
        "Crear un sistema de monitoreo que permita optimizar el consumo de energía."
      ]
    },
    "objetivos_especificos": [
      {
        "objetivo": "Identificar los puntos de mayor consumo.",
        "aprobado": "SI",
        "detalle": "Correcto. Verbo inicial de conocimiento, aunque le falta especificar el cómo y el para qué para ser más robusto.",
        "sugerencias": "El objetivo es claro pero podría ser más completo.",
        "opciones_de_sugerencias": []
      }
    ]
  }
}

### OBJETIVOS A EVALUAR ###
[AQUÍ VA EL JSON CON LOS OBJETIVOS DEL ESTUDIANTE]
```


### Ejemplo:
llama3.1, llama3.3
deepseek-r1:14b
gemma3:270m
qwen

#### Objetivos
```
Aumentar la competitividad de la empresa mejorando la Productividad y Calidad de sus operaciones, mediante la planeación, medición, análisis y mejora de sus procesos, teniendo como base fundamental el uso y la aplicación de modelos estadísticos. 

Aumentar el índice de productividad del departamento X en un 15% para diciembre de 2024, implementando un sistema de control basado en modelos estadísticos.

Reducir la tasa de defectos en el proceso Y a menos del 3% dentro de los próximos tres meses mediante análisis estadístico y aplicación de controles calidad.

Aumentar la satisfacción del cliente en un 15% para el tercer trimestre de 2025, implementando un nuevo sistema de soporte en línea y capacitando al equipo de atención al cliente.


• Establecer una estructura horizontal mediante el enfoque de procesos 
• Establecer una matriz de indicadores que permita controlar y mejorar los procesos 
• Establecer un control estadístico de procesos para las operaciones en la obtención 
del alimento balanceado. 
• Determinar que mediante el análisis sistemático de los procesos se puede mejorar la 
productividad de la organización.

Desarrollar un diseño que permita la visualización de la curva I-V de un panel PV mediante la implementación de un método práctico, programable, para que pueda ser replicado por estudiantes de pregrado.

• Desarrollar un procedimiento para la determinación de la curva de operación I-V para la obtención de mediciones de forma automática.
• Diseñar un prototipo escalable basado en el método seleccionado para el trazador de curvas I-V
• Realizar las mediciones de corriente y voltaje de un panel PV que nos permitan la adquisición diferentes puntos de la curva.

Optimizar la gestión de costos en la Escuela de Organización Integral de Eventos de FCSH-ESPOL, por medio de la aplicación de un sistema que permita la distribución, registro y análisis de los costos de manera precisa, mejorando la toma de decisiones financieras y garantizando sostenibilidad de la Escuela.

1. Realizar una revisión de fundamentos teóricos y casos de estudio sobre los principales modelos para la estimación de costos en organizaciones similares para poder identificar las mejores prácticas.
2. Diagnosticar la situación actual de la gestión de costos en la EOIE, identificando debilidades en el registro, distribución y control de costos directos e indirectos, así como la precisión de la información financiera utilizada en la toma de decisiones.
3. Evaluar el impacto del sistema de costeo en la rentabilidad y sostenibilidad de la Escuela, mediante un informe detallado que compare la situación antes y después de su implementación. 
```

#### Prompt usado
```
Aumentar la satisfacción del cliente en un 15% para el tercer trimestre de 2025, implementando un nuevo sistema de soporte en línea y capacitando al equipo de atención al cliente.
```

##### deepseek-r1 6m 4.0s
```
<think>
Hmm, the user wants me to act as a thesis academic objective evaluator and assess whether a given objective is properly formulated according to specific criteria from Bloom's taxonomy.

They've provided an objective about increasing client satisfaction by implementing new systems and training staff. I need to evaluate if it starts with a single infinitive verb from Bloom's taxonomy, doesn't have multiple verbs in the infinitive form, and clearly answers what (main action), how (method/activities) and for what (purpose/impact).

Looking at this objective: "Aumentar la satisfacción del cliente en un 15% para el tercer trimestre de 2025, implementando un nuevo sistema de soporte en línea y capacitando al equipo de atención al cliente." 

I notice there are two infinitive verbs here - "Aumentar" and "Implementando". While the main goal is to increase client satisfaction, it includes an additional action of implementing a system. This violates criterion number 2.

The user mentioned that in academic contexts like production or design projects, responding to all three questions (what, how, for what) isn't necessary. However, their first two criteria about verb usage still apply - there should be only one infinitive verb at the beginning of the objective.

For my response format, I need to use exactly this JSON structure: {"aprobado": "SI" | "NO", "verbos": ["..."], "detalle": "...", "sugerencias": "...", "opciones de sugerencias": ["", "", ""]} 

Since it doesn't meet the criteria (multiple verbs), I'll mark "aprobado" as "NO". In the verbos field, I should list both problematic verbs - ["Aumentar", "Implementando"].

For the detalle section, I need to explain clearly what's wrong with this objective. The main issue is having multiple infinitive verbs in a single goal statement.

In sugerencias, I can suggest making it clearer by specifying that the implementation is part of achieving the satisfaction increase - perhaps stating how these actions will contribute to the 15% increase.

For opciones de sugerencias, since there are three required examples but only one verb should be used, I need to create three alternative objectives. The first could focus solely on increasing satisfaction with a clear method. Second might combine both goals properly using an infinitive conjunction like "incrementar y mejorar". Third would use another Bloom's action verb appropriately.

The user needs this evaluation for academic thesis work in production or design fields. They're likely looking to ensure their research objectives are correctly formulated before proceeding, so being thorough with my suggestions could help them avoid future mistakes.
</think>

json
{
  "aprobado": "NO",
  "verbos": ["Aumentar", "Implementando"],
  "detalle": "El objetivo contiene dos verbos en infinitivo: 'Aumentar' y 'Implementando'. Esto no está permitido, ya que un objetivo académico debe comenzar con un único verbo de acción.",
  "sugerencias": "Para mayor claridad semántica, elige uno solo como núcleo del objetivo. Por ejemplo: si se desea medir la mejora específica derivada de las capacitaciones y el nuevo sistema, podrías redefinir el objetivo para centrarse en esa relación causal.",
  "opciones de sugerencias": [
    "Objetivo formulado correctamente siguiendo los criterios: 'Incrementar la satisfacción del cliente mediante la implementación y capacitación adecuada relacionada con un nuevo sistema de soporte en línea, logrando una mejora del 15% para el tercer trimestre de 2025'.",
    "Ejemplo alternativo que responde a qué (satisfacción), cómo (medir por encuestas) y para qué: 'Medir la satisfacción del cliente mediante un cuestionario en línea, aplicado dos veces al año, con el propósito de evaluar su evolución temporal'.",
    "Objetivo bien formulado siguiendo los criterios: 'Determinar las relaciones causa-efecto entre la implementación del sistema de soporte en línea y el cambio en la satisfacción del cliente durante el tercer trimestre de 2025, mediante análisis estadístico de encuestas pre-posadas'."
  ]
}
```

##### deepseek-r1:1.5b  1m 31s
```
<think>
Okay, let me try to figure out if this objective is correctly formulated. The user provided a Spanish objective in English and wants me to evaluate its correctness as an academic thesis objective. They also want it presented in JSON format with detailed explanations.

First, I need to understand what each part of the JSON should contain. The main fields are "aprobado" (whether it's correct or not), "verbos" (the verb in infinitive and any others), "detalle" for what's missing, "sugerencias" (what needs improvement if there's a problem), and "opciones de sugerencia" (alternatives if it's incorrect).

The objective is: “Aumentar la satisfacción del cliente en un 15% para el tercer trimestre de 2025, implementando un nuevo sistema de soporte en línea y capacitando al equipo de atención al cliente.”

Breaking it down:
- "Aumentar la satisfacción" – verb in infinitive.
- The rest are additional verbs for implementation and capacity.

The question is correctly answered by the verb "aumentar." The method/strategy/inactions (new system, new support) are given. The purpose (increasing satisfaction by 15% in Q3 2025) seems covered. No missing part on impact, so detail might say it's correct.

But wait, is the objective too vague? It mentions an increase of 15%, but what if it's a small percentage? Maybe better to be specific. Also, including "capacitating al cliente" could suggest they're considering customer needs beyond just clients. That might make it clearer about the goal's scope.

So, I should adjust for clarity and completeness. Instead of vague percentages, maybe specify that it's an average increase or something concrete like 10%. That would make it more precise but still cover the main points. Then, in detail, perhaps mention increasing satisfaction by X% over three quarters and why this matter.

Also, ensuring all parts are covered: question, method, purpose, impact. Since there’s no mention of consequences (like financial results), maybe leave that as a note or adjust accordingly.

Overall, I'll suggest an improved objective and explain the changes made in detail, including any necessary adjustments to ensure clarity without being too specific.
</think>

json
{
  "aprobado": "SI",
  "verbos": ["Aumentar", "capacitating", "sistema", "soporte"],
  "detalle": {
    "detalles": {
      "cruzigada": "La objetivo está bien formulada, claramente detallada. Se refleja claramente el propósito (incremento de satisfiacción al 15% en Q3 2025), la meta principal (capacitación al cliente y sistema de soporte), las estrategias (implementar un sistema lineal, capacitarse al cliente) y su consecuencia (satisfacción aumentada) por lo que puede importar la calidad final."
    }
  },
  "sugerencias": {["La objetivo es claramente definida. Puedes mejorar el diálogo para que muestre mejor los objetivos", "Introducir una metrica más clara para el aumento de satisfiacción, por ejemplo, un incremento de X% en Q3 2025.", "Reconocer si el aumento de satisfiacción está equilibrado con otros aspectos del proyecto"]
  },
  "opciones de sugerencia": []
}
```

##### deepseek-r1:7b  5m 48s
```
<think>
Okay, I need to evaluate the given objective according to the criteria provided. Let me start by reading the objective carefully: "Aumentar la satisfacción del cliente en un 15% para el tercer trimestre de 2025, implementando un nuevo sistema de soporte en línea y capacitando al equipo de atención al cliente."

First, I'll check if it starts with a Bloom's Taxonomy verb. The verbs here are "Aumentar" (increase) and "implementar" (carry out), both in the present tense. Since the first verb is correct, that part is okay.

Next, I need to verify if the objective explicitly answers the three questions: ¿Qué?, ¿Cómo?, y ¿Para qué?. 

- ¿Qué?: The action seems to be increasing customer satisfaction by 15%.
- ¿Cómo?: They plan to implement an online support system and train the customer service team.
- ¿Para qué?: The goal is to achieve a 15% increase in client satisfaction for the third quarter of 2025.

The objective does cover all three aspects, so that's good.

Now, considering the context. This is for a graduation thesis in an engineering or design-related program. It makes sense as they're likely working on improving customer service systems within their field.

Looking at clarity and specific objectives: The goal of 15% over a specific timeframe is clear. However, the objective doesn't specify how this increase will be measured or what benchmarks are used. Without that detail, it's a bit vague. Also, while they mention implementing a new system and training, there's no indication of how these actions directly contribute to improving satisfaction.

So, two main issues: lack of specificity in measurement (e.g., percentage increase from where) and missing context on the methods' effectiveness beyond implementation.
</think>

json
{
  "aprobado": "NO",
  "verbos": ["aumentar"],
  "detalle": "El objetivo no es específico en cuanto a cómo se midrá el aumento de satisfacción del cliente y carece de claridad sobre los objetivos específicos y las methologías para alcanzar el propósito. Se sugiere incluir detalles como la medición del impacto y los indicadores quantitativos.",
  "sugerencias": "Incluir medidas cuantitativas, como un increase en comparación con un benchmark establecido y mencionar cómo se medirá la satisfacción del cliente, será esencial para el objetivo.",
  "opciones_de_sugerencias": ["Mejorar la medibilidad del aumento de satisfacción mediante indicadores específicos", "Incluir detalles sobre los indicadores de rendimiento relacionados con la satisfacción del cliente", "Detallar las metas intermedias de mejora en el sistema de soporte"]
}
```

