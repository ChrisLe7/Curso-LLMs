# Resumen de la Clase 3 – Herramientas y Plataformas Basadas en LLMs

Esta tercera sesión del curso **“LLMs en Programación: De la Generación de Código a la Solución de Problemas”** se centra en el ecosistema de herramientas basadas en LLMs, desde asistentes en la nube como GitHub Copilot o ChatGPT hasta la instalación de modelos locales con Ollama y alternativas como LM Studio o Text Generation WebUI.

## 1. Introducción

* Los LLMs se integran en entornos de programación mediante distintas plataformas.
* El objetivo de la sesión es **comparar herramientas**, entender sus ventajas y limitaciones, y practicar con ellas en tareas de desarrollo.

## 2. GitHub Copilot

* **Qué es**: asistente de autocompletado y generación de código integrado en editores como VSCode.
* **Cómo funciona**: sugiere código en función del contexto del archivo/proyecto.
* **Beneficios**:

  * Aceleración en tareas repetitivas.
  * Mejores prácticas y código idiomático.
  * Integración fluida en el IDE.
* **Limitaciones**:

  * Contexto reducido al archivo actual.
  * Puede inducir errores sutiles.
  * No explica alternativas.
* **Casos de uso**:

  * Autocompletado inteligente de funciones.
  * Generación de pruebas unitarias.
  * Conversión de código entre lenguajes.
  * Documentación automática.

## 3. ChatGPT y APIs de OpenAI

* **Qué es**: modelo conversacional para depurar, refactorizar y generar código.
* **Ventajas**: interacción flexible, versatilidad en aplicaciones, acceso sencillo (web/API).
* **Limitaciones**: riesgo de alucinaciones, control limitado sobre el formato de salida, coste asociado a la suscripción.
* **Casos de uso**:

  * Explicación de código legado.
  * Refactorización y mejora de estilo.
  * Diseño de arquitecturas y patrones.
  * Generación de scripts de configuración (Dockerfile, GitHub Actions, etc.).

## 4. LLMs en local

* **Por qué ejecutarlos localmente**:

  * Mayor privacidad (los datos no salen de la máquina).
  * Uso offline y baja latencia.
  * Flexibilidad y coste cero (más allá del hardware).
* **Herramientas populares**:

  * **Ollama**: CLI para descargar y ejecutar modelos (LLaMA, Mistral, Gemma, CodeLlama…). Expone API HTTP local (`http://localhost:11434`).
  * **LM Studio**: GUI para descargar, probar y chatear con modelos en CPU/GPU.
  * **Text Generation WebUI**: entorno web para gestionar modelos, con instalación más avanzada.
  * **CodeGPT**: extensión para VSCode que conecta con APIs (OpenAI, HuggingFace, Anthropic) y con endpoints locales como Ollama.
* **Comparación nube vs local**:

  * Nube: acceso inmediato a modelos grandes (GPT-4, Claude, Gemini), sin consumo de recursos locales.
  * Local: privacidad total, latencia mínima, pero requiere hardware (CPU/GPU y espacio en disco).

## 5. Actividad práctica

* Comparación entre Copilot y ChatGPT con el mismo prompt:

  > *“Genera una función en Python que lea un archivo CSV y calcule el promedio por columna numérica.”*
* Discusión posterior: diferencias de estilo, manejo de errores y casos en que conviene cada herramienta.

## 6. Conclusiones

* No hay una “mejor herramienta universal”: la elección depende del contexto (privacidad, recursos, tipo de tarea).
* Copilot destaca en autocompletado dentro del IDE.
* ChatGPT es más flexible para explicaciones, diseño y generación de scripts.
* Los LLMs locales (Ollama, LM Studio) son clave en proyectos sensibles o sin conexión.

---

## Material adicional

* **Manual de instalación de Ollama** (incluido en la carpeta de recursos):

  * Explica instalación en macOS, Windows, Linux y Docker.
  * Conceptos básicos: tokens, contexto, cuantización, GGUF.
  * Cómo descargar, ejecutar y verificar modelos (`ollama pull`, `ollama run`).
  * Opciones para configurar almacenamiento, exponer API, ejecutar como servicio o contenedor.
  * Buenas prácticas: persistencia de modelos, logs y seguridad al exponer la API.

* **Web oficial de Ollama**: [https://ollama.com](https://ollama.com)

* **LM Studio**: [https://lmstudio.ai](https://lmstudio.ai)

* **Extensión CodeGPT para VSCode**: [https://github.com/CodeGPT-org/CodeGPT-vscode](https://github.com/CodeGPT-org/CodeGPT-vscode)

---

👉 **Próxima sesión (Clase 4):** *Ética, riesgos y buenas prácticas con LLMs en desarrollo de software*.
