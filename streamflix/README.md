# StreamFlix — Recomendador inteligente de películas y series

Plataforma de streaming que recomienda contenido personalizado a cada usuario según su historial, calificaciones y géneros preferidos.

> Proyecto de curso construido con agentes de IA siguiendo una metodología: **primero se diseña (docs/), después se programa tarea por tarea con tests**.

## Estructura del proyecto

```
streamflix/
├── AGENTS.md            # Reglas para la IA en este proyecto
├── README.md            # Este archivo (la estructura definida acá tiene prioridad)
├── docs/
│   ├── idea.md              # Problema, usuarios y objetivo
│   ├── spec.md              # Especificación: reglas de negocio (RN) e historias (HU)
│   ├── plan.md              # Plan técnico y arquitectura
│   ├── tasks.md             # Tareas por etapas con criterios de "terminada cuando"
│   ├── decisiones.md        # Decisiones tomadas y por qué
│   ├── glosario.md          # Términos del dominio
│   ├── preguntas-abiertas.md# Lo que falta definir
│   └── pruebas-agente.md    # Preguntas para comprobar que el agente no inventa
├── backend/             # API (Node.js + TypeScript + Express + Vitest)
└── frontend/            # Interfaz (React + Vite)
```

## Origen de la información (leyenda)

Cada documento indica de dónde sale cada dato, para poder revisarlo:

| Etiqueta | Significa |
|---|---|
| **[TP3]** | Sale del TP N.º 3 (automatización de StreamFlix, 8 preguntas) |
| **[TP4]** | Sale del TP N.º 4 (backend de StreamFlix) |
| **[TP1]** | Sale del TP N.º 1 (FlowPulse): tecnologías y formato de SPEC |
| **[AGENTS]** | Sale del archivo "Mi primer AGENTS" |
| **[CAPTURA]** | Sale del ejemplo ReservaClub (formato de tareas y tests) |
| **[PROPUESTA]** | Lo propuso la IA para completar la estructura. **No viene de los TPs: revisar y decidir.** |

## Cómo trabajar (flujo con agentes)

1. Leer `AGENTS.md` y `docs/spec.md`.
2. Tomar **una tarea** de `docs/tasks.md` cuyas dependencias estén en `[x]`.
3. Escribir primero el test, después el código.
4. Cuando se cumple "Terminada cuando", marcar la tarea con `[x]`.
5. Anotar decisiones importantes en `docs/decisiones.md` y dudas en `docs/preguntas-abiertas.md`.

## Puesta en marcha (cuando exista el backend)

```bash
cd backend
cp .env.example .env     # completar los valores
npm install
npm test
npm run dev
```

## Estado

Ver `docs/tasks.md` para el avance por etapa.
