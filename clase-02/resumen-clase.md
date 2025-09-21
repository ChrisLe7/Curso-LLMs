# Resumen de la Clase 2 – Prompt & Context Engineering

Esta segunda sesión del curso **“LLMs en Programación: De la Generación de Código a la Solución de Problemas”** se centra en el diseño de prompts efectivos y en cómo estructurar el contexto para guiar a los modelos hacia respuestas más útiles, precisas y controladas.

## 1. Introducción

* El **Prompt Engineering** es el arte de **escribir instrucciones claras y estructuradas** para un LLM.
* No se trata solo de “qué preguntar”, sino de **cómo enmarcar la pregunta** y **qué contexto proporcionar**.
* Introducción de la noción de **Context Engineering**: organización de ejemplos, instrucciones y referencias para mejorar la calidad de la salida.

## 2. Fundamentos del Prompt Engineering

* **Zero-shot prompting**: pedir al modelo directamente sin ejemplos.
* **One-shot prompting**: dar un único ejemplo para guiar la respuesta.
* **Few-shot prompting**: proporcionar varios ejemplos para que el modelo generalice.
* El estilo de redacción influye en la calidad: instrucciones explícitas y roles definidos (*“actúa como…”*).

## 3. Estrategias avanzadas

* **Chain-of-thought prompting**: inducir razonamientos paso a paso.
* **Self-consistency**: generar múltiples respuestas y elegir la más consistente.
* **Role prompting**: asignar al modelo un papel concreto (ej. *“Eres un profesor de Python”*).
* **Reflexive prompting**: pedir al modelo que revise o critique su propia salida.
* **Prompt chaining**: dividir tareas complejas en pasos encadenados.

## 4. Context Engineering

* Uso de **instrucciones globales** para orientar todo el flujo de la conversación.
* Incorporar **ejemplos relevantes** para que el modelo aprenda en contexto.
* **Formatos de salida predefinidos** (JSON, tablas, Markdown) para obtener respuestas estructuradas.
* Técnicas de **gestión de memoria**: dividir contexto largo, resúmenes parciales, embeddings.

## 5. Limitaciones y riesgos

* **Alucinaciones**: incluso con buenos prompts, el modelo puede inventar información.
* **Sobrecarga de contexto**: demasiados ejemplos o datos irrelevantes reducen la precisión.
* Riesgos de **dependencia excesiva** en prompts diseñados por terceros.
* Sesgos presentes en el entrenamiento pueden amplificarse por prompts mal diseñados.

## 6. Parte práctica

* Ejercicios en clase sobre diseño de prompts:

  * Transformar un prompt vago en uno claro y detallado.
  * Comparar resultados entre **zero-shot** y **few-shot**.
  * Uso de formato estructurado (ej. JSON) para controlar la salida.
* Dinámicas grupales: los estudiantes diseñan prompts para problemas de programación y luego analizan las diferencias de resultados.

## 7. Conclusiones de la clase

* Los **LLMs no entienden**, pero responden mejor si les damos **instrucciones precisas**.
* El diseño del prompt es una **habilidad crítica** para aprovechar al máximo estas herramientas.
* El **contexto bien gestionado** multiplica la calidad de las respuestas.
* Prompt y Context Engineering son la base de aplicaciones más avanzadas (RAG, fine-tuning, agentes).

---

## Material adicional

Para reforzar lo aprendido en esta clase se recomienda revisar:

* **Guía visual sobre Prompt Engineering** (carpeta `material_adicional`).
* **Ejemplos prácticos de prompts efectivos** incluidos como recursos adicionales.
* **Artículo de referencia**: *Prompt Engineering Techniques for Large Language Models* (2023).
* **Paper “How People Use ChatGPT” (Chatterji et al., 2025)**: un estudio a gran escala sobre los patrones de uso real de ChatGPT en más de 700 millones de usuarios. Sus hallazgos principales:
    - El 70% de los mensajes ya no están relacionados con el trabajo, sino con usos personales.
    - Los tres temas más frecuentes son Practical Guidance, Writing y Seeking Information (casi el 80% del total).
    - Writing domina en entornos laborales, sobre todo para editar, resumir o traducir textos.
    - El uso laboral es más común en perfiles educados y profesionales, mientras que el uso recreativo crece más en jóvenes y en países de renta media-baja.

---

👉 **Próxima sesión (Clase 3):** *Herramientas y plataformas basadas en LLMs (local vs nube)* — exploraremos entornos prácticos como ChatGPT, Claude, Gemini, Copilot y soluciones open-source.
