# Curso: LLMs para Programación — Edición Septiembre

Repositorio del curso "LLMs en Programación: De la generación de código a la solución de problemas", con el material del curso (diapositivas, guías, prácticas y recursos útiles). El contenido se irá incorporando progresivamente a lo largo de las sesiones.

## Objetivos del curso

* Entender qué son los LLMs y cómo funcionan a alto nivel.
* Aplicar LLMs a tareas de desarrollo (redacción técnica, ayuda al código, pruebas, refactor).
* Desarrollar el criterio de decisión: ¿cuándo utilizar prompting, RAG o fine-tuning?
* Practicar buenas prácticas, seguridad y evaluación.

## Estructura del repositorio

```
.
├── clase-01/
│   ├── diapositivas/                # PDF/Beamer de la Clase 1
│   └── recursos/                    # Archivos auxiliares (opc.)
├── clase-02/                        # (placeholder)
├── clase-03/                        # (placeholder)
└── README.md
```

> Nota: Los directorios de Clases 4–7 se añadirán conforme avance el curso.

---

## Clase 1 — Introducción a la IA Generativa y LLMs

* Diapositivas: `clase-01/diapositivas/Diapositivas-Clase-1-Edicion-Septiembre.pdf`
* Formato: teórico + demostraciones guiadas
* Instalación requerida: ninguna (se verán modelos locales en Clase 3)

### Enlaces interesantes (Clase 1)

1. Blog visual sobre la evolución de los LLMs:
   [https://goyalpramod.github.io/blogs/evolution\_of\_LLMs](https://goyalpramod.github.io/blogs/evolution_of_LLMs)
2. Survey de LLMs (arXiv):
   [https://arxiv.org/html/2303.18223v16](https://arxiv.org/html/2303.18223v16)

### (Opcional) Formulario inicial de usos de IA

* Propósito: recoger 3 usos reales que ya haces con IA y 1 preocupación o duda.
* Enlace del formulario: [https://forms.gle/XqRpFih5T7dDgDPW6](https://forms.gle/XqRpFih5T7dDgDPW6)
* Se utilizará para adaptar ejemplos y casos en clases posteriores.

---

## Clase 2 — Prompt & Context Engineering

* Diapositivas: `clase-02/diapositivas/Diapositivas-Clase-2-Edicion-Septiembre.pdf`
* Formato: teórico + ejercicios prácticos de diseño de prompts
* Instalación requerida: ninguna (se trabaja sobre interfaces LLM en navegador)

En esta sesión se profundiza en **cómo guiar a los LLMs mediante prompts claros y contextos bien estructurados**. 

Se cubren técnicas desde lo básico (*zero-shot, one-shot, few-shot*) hasta estrategias avanzadas como *chain-of-thought*, *prompt chaining* o *role prompting*.  

La práctica se centra en **transformar prompts vagos en instrucciones precisas** y analizar cómo cambia la calidad de las respuestas según la técnica utilizada. También se introduce el concepto de **Context Engineering**, clave para aplicaciones más complejas.

### Enlaces interesantes (Clase 2)

1. Guía visual de Prompt Engineering (incluida en `material_adicional/`).  
2. Artículo: *Prompt Engineering Techniques for Large Language Models* (2023).  
3. Paper: *How People Use ChatGPT* (Chatterji et al., 2025).  
   Estudio empírico sobre más de 700M de usuarios que revela patrones de uso reales:  
   - El 70% de interacciones son personales, no laborales.  
   - Los temas dominantes son *Writing*, *Practical Guidance* y *Seeking Information*.  
   - El uso profesional se concentra en tareas de edición, traducción y redacción técnica.  


---

## Roadmap (resumen)

* Clase 1: qué es un LLM, casos de uso, demos, riesgos/beneficios.
* Clase 2: Prompt & Context Engineering (mejorar especificaciones, tests en el prompt).
* Clase 3: Modelos locales (instalación y puesta en marcha).
* Clase 4–7: RAG / evaluación / prácticas integradas (se detallará).


---

## Cómo usar este repo

1. Descarga o clona el repositorio.
2. Abre `clase-01/diapositivas/` y revisa el PDF de la sesión.
3. Consulta los enlaces de “Clase 1” para ampliar.

---

## Requisitos (generales del curso)

* Navegador actualizado.
* Para sesiones prácticas futuras: Python 3.11+, `pip`, y editor (VS Code / PyCharm).
* Instrucciones concretas se incluirán en cada clase.

---

## Contribuir / Feedback

* Abre un Issue con sugerencias, erratas o dudas.
* Pull Requests bienvenidos para *typos* o mejoras menores.
* Si eres alumno: indica el número de clase y la diapositiva/actividad afectada.

---

## Licencia

Por definir. (Se añadirá al publicarse el material completo.)

> Si vas a reutilizar contenidos, respeta las licencias de fuentes externas citadas en los materiales.

---

## Contacto

* Profesor del curso: Christian Luna Escudero (c.luna@uco.es)
* Incidencias técnicas del repo: Issues de GitHub

---

### Changelog

* 2025/09/21: Publicada Clase 1 y añadidos enlaces complementarios.
* 2025/09/21: Publicada Clase 2 (Prompt & Context Engineering) y añadidos enlaces complementarios.

"""