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
````
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

### Ejemplo:
llama3.1, llama3.3
deepseek-r1:14b
gemma3:270m
qwen

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


2:11 a 2:15 pensando a 2:19
2:30 a 2:32 - 1:45 pensando a 2:34 - 1:50
2:38 para cargar comienza a escribir 

- 8 de ram para 7B de parametros
- 16 de ram para 13B de parametros
- 32 de ram para 33B de parametros
- 13 ram para 20B

### Prompt usado
```
Aumentar la satisfacción del cliente en un 15% para el tercer trimestre de 2025, implementando un nuevo sistema de soporte en línea y capacitando al equipo de atención al cliente.
```

####
```

```

#### deepseek-r1 6m 4.0s
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

#### deepseek-r1:1.5b  1m 31s
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

#### deepseek-r1:7b  5m 48s
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

Linux

Editar el servicio Systemd:
Abra una terminal y ejecute systemctl edit olama.service.
Agregue la línea Environment="OLLAMA_MODELS=/path/to/new/location" en la sección [Servicio].
Guardar y salir del editor.
Recargar y reiniciar:
Ejecute systemctl daemon-reload.
Reinicie Ollama con systemctl restart ollama.





$ ollama serve --help
Variables de Entorno:

OLLAMA_HOST El host:puerto al que conectarse (predeterminado "127.0.0.1:11434")

OLLAMA_ORIGINS Una lista separada por comas de orígenes permitidos.

OLLAMA_MODELS La ruta al directorio de modelos (predeterminado es "~/.ollama/models")

OLLAMA_KEEP_ALIVE La duración que los modelos permanecen cargados en memoria (predeterminado es "5m")

Si instalaste ollama automáticamente como se indica en el archivo Léame:
abre el archivo systemd

$ sudo nano /etc/systemd/system/ollama.service

agrega Environment="OLLAMA_MODELS=/tu/ruta/deseada" debajo de [Service]

[Service]
ExecStart=$BINDIR/ollama serve
User=ollama
Group=ollama
Restart=always
RestartSec=3
Environment="PATH=$PATH"
Environment="OLLAMA_MODELS=/tu/ruta/deseada" #agregarás esta línea
presiona CTRL+X luego Y luego Enter

$ systemctl daemon-reload
$ systemctl restart ollama

esto debería funcionar.

Si no:
todo lo que tienes que hacer es configurar la variable de entorno OLLAMA_MODELS antes de ejecutar ollama.

$ export OLLAMA_MODELS=/tu/ruta/deseada
$ ollama serve