# StreamFlix — Decisiones

Formato: qué propuso la IA, qué decidí yo y por qué.

## D-01 — Recomendaciones sin IA externa en la v1
**Origen:** [TP4] (la decisión de la IA que cuestionaste).
- **Propuesta inicial:** usar una herramienta externa de IA para generar todas las recomendaciones desde el comienzo.
- **Decisión:** empezar con un sistema simple basado en géneros preferidos e historial.
- **Por qué:** es más fácil de implementar y probar. Cuando haya más usuarios y datos se puede sumar IA más avanzada.

## D-02 — Arquitectura por capas
**Origen:** [TP4] (arquitectura elegida).
- **Decisión:** Controller → Service → Repository.
- **Por qué:** cada parte tiene una función específica y es más fácil de mantener y probar.

## D-03 — Una calificación por usuario y contenido
**Origen:** [PROPUESTA] — no está en tus TPs. Confirmá si la querés.
- **Decisión:** volver a calificar actualiza el puntaje existente.
- **Por qué:** evita duplicados y mantiene limpias las recomendaciones.

## D-04 — Trabajo por tareas con criterios verificables
**Origen:** [PROPUESTA] basada en el formato de [CAPTURA] y en [AGENTS] sección 5. Confirmá si la querés.
- **Decisión:** cada tarea de `tasks.md` tiene "Terminada cuando" y solo se marca con `[x]` si los tests lo confirman.
- **Por qué:** evita dar por terminado algo que no funciona.

## Plantilla para nuevas decisiones
```
## D-0X — Título
- Propuesta de la IA:
- Mi decisión:
- Por qué:
```
