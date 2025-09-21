# Resumen de la Clase 1 – Fundamentos de los LLMs

Esta primera sesión del curso **“LLMs en Programación: De la Generación de Código a la Solución de Problemas”** introduce los conceptos básicos de los **Grandes Modelos de Lenguaje (LLMs)**, su evolución histórica, su arquitectura técnica y su aplicación práctica en el ámbito de la programación.

## 1. Introducción a la Inteligencia Artificial y los LLMs

* La IA tiene un doble objetivo: **tecnológico** (crear sistemas capaces de realizar tareas inteligentes) y **científico** (comprender los fundamentos del comportamiento inteligente).
* La IA ya está presente en numerosos ámbitos: generación automática de texto, asistentes virtuales, diagnóstico médico, detección de fraudes, automatización industrial, etc.
* Los **LLMs** son modelos entrenados con grandes volúmenes de texto y código, capaces de predecir la siguiente palabra en una secuencia y de capturar patrones complejos del lenguaje.

## 2. Evolución histórica de los modelos de lenguaje

* **Años 90–2000:** modelos estadísticos basados en n-gramas.
* **2000s:** redes neuronales recurrentes (RNN) y sus variantes LSTM y GRU, capaces de modelar dependencias a largo plazo.
* **2014–2017:** arquitecturas seq2seq y encoder-decoder para traducción y resumen automático.
* **2017:** aparición del **Transformer**, que marcó un hito por su paralelización, atención múltiple y escalabilidad.
* **2018–2025:** explosión de modelos como GPT-2, GPT-3, Codex, GPT-4, LLaMA, Gemini, DeepSeek, hasta los más recientes optimizados para programación y razonamiento.

## 3. Arquitectura y capacidades de los LLMs

* Componentes clave: **tokenización, embeddings, capas de atención y redes apiladas**.
* La **auto-atención** permite que cada token valore su relación con el resto del contexto.
* La **escalabilidad** (más parámetros y datos) habilita capacidades emergentes como:

  * *Chain-of-thought* (razonamiento paso a paso).
  * *In-context learning* (aprender de ejemplos en el prompt).
  * Uso de herramientas externas (APIs, cálculos).
* El tamaño del modelo determina un salto cualitativo en las tareas que puede realizar.

## 4. Aplicaciones en programación

Los LLMs resultan especialmente útiles porque el código fuente es un lenguaje estructurado y abundante en repositorios públicos. Entre sus aplicaciones:

* Autocompletado inteligente (ej. GitHub Copilot, Amazon CodeWhisperer).
* Generación de funciones a partir de descripciones en lenguaje natural.
* Explicación, documentación y refactorización de código.
* Creación de pruebas unitarias y casos de test.
* Depuración asistida y sugerencias de buenas prácticas.

Se revisaron casos específicos para desarrolladores **backend**, **frontend**, **ingeniería de datos** e **investigación en ML**.

## 5. Limitaciones y riesgos

* Los modelos no “entienden” el propósito: solo predicen tokens.
* Posibles **alucinaciones** (funciones o imports inexistentes).
* Dificultad con proyectos grandes y dependencias múltiples.
* Riesgos de seguridad (fugas de datos, licencias, vulnerabilidades).
* Dependencia excesiva que puede reducir la comprensión del programador.

## 6. Impacto, productividad y ética

* Estudios muestran mejoras de hasta **+55 % en velocidad de desarrollo** al usar asistentes de código.
* Los LLMs **no sustituyen al programador**, sino que aumentan su productividad y reducen la barrera de entrada.
* Consideraciones éticas: sesgos en datos, privacidad, copyright y responsabilidad del uso del código generado.
* Buenas prácticas: verificar resultados, diseñar prompts claros, documentar el uso de las sugerencias.

## 7. Evaluación de LLMs en programación

* Benchmarks como **HumanEval**, **MBPP**, **Bugs-BUSTED** o **SWE-Bench** permiten medir precisión, generalización y capacidad de corrección.
* Métricas como **Pass\@k** ayudan a evaluar la probabilidad de obtener soluciones correctas en múltiples intentos.

## 8. Parte práctica

* Ejemplo de generación de código con ChatGPT/Copilot, mostrando la importancia de refinar los prompts.
* Ejercicio en clase: escribir un prompt para generar una función que determine si un número es primo, con manejo de errores y comentarios.

## 9. Conclusiones de la clase

* Los LLMs funcionan prediciendo tokens y capturando patrones gracias a la arquitectura Transformer.
* Su evolución histórica y escalado han permitido la aparición de capacidades emergentes.
* En programación, ofrecen grandes beneficios en productividad, pero también presentan riesgos y limitaciones.
* El rol del programador cambia hacia un uso crítico y supervisado de estas herramientas.

---

👉 **Próxima sesión (Clase 2):** *Prompt Engineering aplicado a programación* — fundamentos (zero-shot, one-shot, few-shot), diseño de prompts efectivos y casos prácticos.

--- 


## Material adicional

Para complementar la clase, se recomienda revisar los siguientes recursos:

* **Blog visual sobre la evolución de los LLMs**
  [https://goyalpramod.github.io/blogs/evolution\_of\_LLMs](https://goyalpramod.github.io/blogs/evolution_of_LLMs)

* **Survey de LLMs (arXiv, 2023)**
  [https://arxiv.org/html/2303.18223v16](https://arxiv.org/html/2303.18223v16)

* **Video canal DotCSV: ¿Por qué estas REDES NEURONALES son tan POTENTES? 🤔 | TRANSFORMERS Parte 2**
  [https://www.youtube.com/watch?v=xi94v\_jl26U](https://www.youtube.com/watch?v=xi94v_jl26U)

* **Artículo académico de referencia**
  *History, development, and principles of large language models: an introductory survey* (AI & Ethics, 2025).
  Este trabajo ofrece una visión accesible sobre la evolución, principios, aplicaciones, limitaciones y futuros desafíos de los LLMs.