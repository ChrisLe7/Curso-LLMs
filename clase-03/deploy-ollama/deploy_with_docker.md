# Despliegue Ollama + Open WebUI (GPU) sin docker-compose

> **Escenario:** máquina con Docker y NVIDIA Container Toolkit, **sin** `docker compose`/`docker-compose`.
> **Objetivo:** levantar **Ollama** (API local) y **Open WebUI** (interfaz web) usando **GPU NVIDIA** y volúmenes locales.

## 0) Preparación

```bash
# 0.1) Persistencia local (junto a esta carpeta)
mkdir -p ollama openwebui
# 1cf30ff78328055a556a0ed641105cd2aa11f36765356705dffdfb150d444540
# 0.2) Red Docker para resolver contenedores por nombre
docker network create llmnet
```

---

## 1) Levantar **Ollama** con GPU

> Elige **A** (moderno: `--gpus`) o **B** (runtime clásico: `--runtime=nvidia`). Usa **una** de las dos.

### A) Docker moderno (`--gpus`)

```bash
docker run -d \
  --name ollama \
  --gpus all \
  --network llmnet \
  -p 11434:11434 \
  -e OLLAMA_HOST=0.0.0.0:11434 \
  -v "$(pwd)/ollama:/root/.ollama" \
  --restart unless-stopped \
  ollama/ollama:latest
```

### B) Docker con runtime NVIDIA clásico

```bash
docker run -d \
  --name ollama \
  --runtime=nvidia \
  -e NVIDIA_VISIBLE_DEVICES=all \
  -e NVIDIA_DRIVER_CAPABILITIES=compute,utility \
  --network llmnet \
  -p 11434:11434 \
  -e OLLAMA_HOST=0.0.0.0:11434 \
  -v "$(pwd)/ollama:/root/.ollama" \
  --restart unless-stopped \
  ollama/ollama:latest
```

**Checks rápidos**

```bash
# ¿Responde la API?
curl -sf http://localhost:11434/api/tags && echo "OK"

# ¿Ve GPUs?
docker exec -it ollama nvidia-smi
```

---

## 2) Limitar cuántas/cuáles GPUs usa el contenedor

### Opción 1 — “Quiero **4 GPUs** (las primeras visibles)”

```bash
docker run -d \
  --name ollama \
  --gpus 4 \
  --network llmnet \
  -p 11434:11434 \
  -e OLLAMA_HOST=0.0.0.0:11434 \
  -v "$(pwd)/ollama:/root/.ollama" \
  --restart unless-stopped \
  ollama/ollama:latest
```

### Opción 2 — “Quiero **IDs concretos** (ej. 0,2,5,7)”

**Con `--gpus` moderno:**

```bash
docker run -d \
  --name ollama \
  --gpus '"device=0,2,5,7"' \
  --network llmnet \
  -p 11434:11434 \
  -e OLLAMA_HOST=0.0.0.0:11434 \
  -v "$(pwd)/ollama:/root/.ollama" \
  --restart unless-stopped \
  ollama/ollama:latest
```

**Con runtime clásico:**

```bash
docker run -d \
  --name ollama \
  --runtime=nvidia \
  -e NVIDIA_VISIBLE_DEVICES=0,2,5,7 \
  -e NVIDIA_DRIVER_CAPABILITIES=compute,utility \
  --network llmnet \
  -p 11434:11434 \
  -e OLLAMA_HOST=0.0.0.0:11434 \
  -v "$(pwd)/ollama:/root/.ollama" \
  --restart unless-stopped \
  ollama/ollama:latest
```

**Verificación**

```bash
docker exec -it ollama nvidia-smi
```

> Debes ver solo las GPUs asignadas.

---

## 3) Descargar modelos (Ollama dentro de Docker)

### 3.1 CLI dentro del contenedor

```bash
docker exec -it ollama ollama pull llama3.2
docker exec -it ollama ollama pull mistral
docker exec -it ollama ollama list
```

> Los modelos/blobs se guardan en `./ollama` (volumen local).

### 3.2 API HTTP (útil para scripts)

```bash
curl -X POST http://localhost:11434/api/pull \
  -H "Content-Type: application/json" \
  -d '{"name":"llama3.2"}'
```

### 3.3 Probar generación rápida (API)

```bash
curl -s -X POST http://localhost:11434/api/generate \
  -H "Content-Type: application/json" \
  -d '{"model":"llama3.2","prompt":"Dime tu nombre en una frase.","stream":false}' | jq .
```

---

## 4) Levantar **Open WebUI** (interfaz gráfica)

```bash
docker run -d \
  --name openwebui \
  --network llmnet \
  -p 3000:8080 \
  -e OLLAMA_BASE_URL=http://ollama:11434 \
  -v "$(pwd)/openwebui:/app/backend/data" \
  --restart unless-stopped \
  ghcr.io/open-webui/open-webui:main
```

* UI en: **[http://localhost:3000](http://localhost:3000)**
* Desde la UI puedes **descargar modelos** (Pull) y chatear con ellos.

---

## 5) Operación diaria

```bash
# Ver logs
docker logs -f ollama
docker logs -f openwebui

# Parar/Arrancar
docker stop openwebui ollama
docker start ollama openwebui

# Actualizar imágenes (no borra tus datos de ./ollama / ./openwebui)
docker pull ollama/ollama:latest
docker pull ghcr.io/open-webui/open-webui:main
docker stop openwebui ollama && docker rm openwebui ollama
# y relanza con los 'docker run' de arriba

# Eliminar todo (no borra tus carpetas locales)
docker stop openwebui ollama && docker rm openwebui ollama
docker network rm llmnet
```

---

## 6) Seguridad y rendimiento (recomendaciones)

* **Exposición local:** si no necesitas acceso externo, publica en loopback:

  ```bash
  -p 127.0.0.1:11434:11434
  -p 127.0.0.1:3000:8080
  ```
* **Espacio en disco:** `./ollama` puede crecer (decenas/centenas de GB). Si necesitas moverlo:

  * Para: `docker stop ollama`
  * Mueve la carpeta a otra unidad y ajusta la ruta en `-v`.
* **Uso compartido (DGX):** limita GPUs por contenedor (sección 2) para evitar acaparar recursos.
* **Salud del servicio:** mantén una sola instancia de Ollama por nodo si compartís GPUs, para evitar thrashing de memoria VRAM.

---

## 7) Diagnóstico rápido

```bash
# 1) API responde
curl -sf http://localhost:11434/api/tags | jq . || curl -sf http://localhost:11434/api/tags

# 2) GPU visible desde el contenedor
docker exec -it ollama nvidia-smi

# 3) Generación mínima
docker exec -it ollama ollama run llama3.2 <<< "Di 'hola' en una palabra."
```

---

## 8) Estructura final

```
llm-stack/
├─ ollama/         # modelos/blobs persistentes (Ollama)
├─ openwebui/      # usuarios, chats, ajustes (UI)
└─ (este README)
```

---

genial, te dejo un bloque **copiable** para añadir al final de tu README (justo después de la sección 3). Incluye: (a) **pool de modelos** recomendados (razonadores y no razonadores), (b) **comandos de descarga** listos para pegar, y (c) un **guion de demo** con prompts para comparar Mac vs DGX y razonador vs no-razonador.

---

## 3.4 Pool de modelos y comandos (razonadores vs no razonadores)

> Objetivo docente: comparar rendimiento/calidad entre tu **Mac** (modelos pequeños) y el **DGX** (V100s), y ver diferencias entre **razonadores** y **no razonadores**.

### Modelos recomendados (para clase)

| Tipo                | Modelo (Ollama tag) | Tamaño aprox. | VRAM estimada | Uso principal                    | Comentario                                                                            |
| ------------------- | ------------------- | ------------: | ------------: | -------------------------------- | ------------------------------------------------------------------------------------- |
| **Generalista**     | `llama3.2:8b`       |            8B |    \~16-18 GB | Baseline general                 | Buen punto de partida; corre en 1×V100 y (con cuantización) en portátiles potentes.   |
| **Generalista**     | `mistral:7b`        |            7B |    \~14-16 GB | QA/resumen                       | Rápido, buena calidad, ideal para comparar con Llama.                                 |
| **Código**          | `codellama:13b`     |           13B |    \~24-26 GB | Generación/explicación de código | Especializado en programación; cabe en 1×V100.                                        |
| **Razonador**       | `deepseek-r1:14b`   |           14B |    \~28-30 GB | Razonamiento paso a paso         | Excelente para “mostrar el salto” en reasoning. Alternativa ligera: `deepseek-r1:8b`. |
| **OSS alternativo** | `gpt-oss:13b`       |           13B |    \~24-26 GB | Generalista OSS                  | Para contrastar arquitecturas/entrenamientos distintos.                               |

> Nota: los consumos son orientativos; dependen de cuantización y build. Si necesitas más holgura, asigna **2–4 GPUs** al contenedor (ver sección 2 del README).

### Comandos de descarga (desde el contenedor de Ollama)

```bash
# Generalistas
docker exec -it ollama ollama pull llama3.2:8b
docker exec -it ollama ollama pull mistral:7b

# Código
docker exec -it ollama ollama pull codellama:13b

# Razonadores (elige uno; 8B para demo rápida, 14B para “wow effect”)
docker exec -it ollama ollama pull deepseek-r1:8b
docker exec -it ollama ollama pull deepseek-r1:14b

# Alternativa OSS (opcional)
docker exec -it ollama ollama pull gpt-oss:13b

# Ver lo instalado
docker exec -it ollama ollama list
```

> Tip: puedes hacer el pull también desde **Open WebUI** (Modelos → Pull), pero con CLI queda en el script de clase y es reproducible.

---

## 3.5 Guion de demo comparativa (listo para clase)

### A) Calentamiento (Mac vs DGX, generalista)

1. **Mac** (p. ej., `llama3.2:3b` u `:8b` si aguanta):
   Prompt:

   > *“Explícame en **4 bullets** qué es un LLM, añade un ejemplo de uso en **Python** y limita la respuesta a **120 palabras**.”*

2. **DGX** (misma instrucción) con `llama3.2:8b` y después `mistral:7b`.
   Objetivo: que vean **latencia** y **calidad** mejoradas.

### B) Razonamiento (razonador vs no razonador)

* **No razonador** (`mistral:7b`) y luego **razonador** (`deepseek-r1:14b`):
  Prompt:

  > *“Tienes 3 depósitos con 120 L, 150 L y 210 L. ¿Cuál es la **capacidad mínima** de garrafas iguales para vaciar **sin sobrar** en ningún depósito? **Explica el razonamiento paso a paso** y da solo el **resultado final** al final en una línea.”*

Observa: el razonador debería verbalizar el **mcd** y pasos intermedios; el no razonador suele acertar pero con menos trazabilidad o más errores.

### C) Programación (especializado vs generalista)

* **codellama:13b** vs `llama3.2:8b`
  Prompt:

  > *“Escribe una función en **Python** `n_primes(n)` que devuelva los **n primeros** números primos. Usa pruebas simples al final y comenta la complejidad. Luego añade una versión con **memoization** si resulta útil.”*

Observa: Codellama tiende a producir **código idiomático** y tests más naturales.

### D) Instrucciones estrictas y formato (context engineering)

* Modelo cualquiera (repite con 2 modelos):
  Prompt:

  > *“Devuélveme **solo JSON** con claves `title` (string), `bullets` (lista de 3 strings), `code` (string con Python) sobre ‘listas por comprensión’. Si no cumples el formato, indica **ERROR**.”*

Objetivo: mostrar control de **formato de salida** y diferencias de robustez.

### E) Medición rápida de latencia con API (opcional)

```bash
time curl -s -X POST http://localhost:11434/api/generate \
  -H "Content-Type: application/json" \
  -d '{"model":"llama3.2:8b","prompt":"Resume en 80 palabras qué es un LLM.","stream":false}' >/dev/null
```

Repite con `mistral:7b` y `deepseek-r1:14b`.

---

## 3.6 Consejos operativos para la práctica

* **Reserva de GPUs** para la sesión “wow”: relanza Ollama con 4–8 GPUs si quieres comparar latencias fuertes (ver sección 2 del README).
* **Memoria**: `codellama:13b` y `deepseek-r1:14b` entran en **1×V100 (32 GB)**, pero si quieres margen y concurrencia, asigna **2–4 GPUs**.
* **Reproductibilidad**: guarda un script `demo.sh` con los `ollama pull` y los `curl` de medición.
* **Seguridad**: si no necesitáis acceso remoto, expón puertos solo en loopback (`127.0.0.1:11434`, `127.0.0.1:3000`).
