# REGLAS DE ORO PARA LA IA EN STREAMFLIX

**Versión:** 1.0

> **Origen:** las secciones 1 a 7 y la zona de peligro salen de **[AGENTS]** ("Mi primer AGENTS"). Lo propio de StreamFlix (arquitectura por capas, bcrypt, JWT, trabajar por tareas, no usar IA externa en la v1) sale de **[TP4]** y **[TP1]**. La sección 8 (responder sin inventar) es **[PROPUESTA]**.

## 1. Contexto y memoria
- **No inventes información.** Si un archivo, función o variable no existe en el proyecto, preguntá. No supongas que existía antes.
- **Leé primero** `README.md` y `docs/spec.md`. La estructura del README tiene prioridad.
- **Trabajá por tareas.** Tomá una sola tarea de `docs/tasks.md`, con dependencias ya cumplidas. No adelantes otras.
- **Si una decisión técnica no está clara**, presentá 2 o 3 opciones con ventajas y desventajas y esperá confirmación.

## 2. Estilo y calidad
- Respetá el estilo del código existente (indentación, nombres, comillas).
- Respetá la arquitectura **Controller → Service → Repository** (ver `docs/plan.md`). Los controllers no acceden a la base de datos y los repositories no contienen reglas de negocio.
- Cada función hace solo lo que dice su nombre.
- No repitas lógica (DRY). Usá TypeScript con tipos explícitos.

## 3. Errores y logs
- Prohibido `catch` vacío. Todo error se registra y se maneja.
- Usá niveles `debug`, `info` y `error`. En producción `debug` va desactivado.
- Los endpoints devuelven códigos HTTP correctos y mensajes de error claros.

## 4. Seguridad y datos
- **Nunca** escribas credenciales en el código. Todo va en `.env` (y `.env.example` solo con nombres, sin valores reales).
- Contraseñas con **bcrypt**. Autenticación con **JWT**.
- Validá todo dato que llegue de un usuario o de una API externa.
- No guardes en logs emails completos, contraseñas ni datos privados.
- Un usuario solo puede ver y modificar **sus propios** datos (RN-02).

## 5. Pruebas
- Cada funcionalidad nueva lleva al menos un test (caso correcto, inválido y límite cuando aplique).
- No bajes la cobertura existente.
- Una tarea solo se marca `[x]` si se cumple su "Terminada cuando".

## 6. Comunicación
- Si no sabés algo, decilo en vez de inventar.
- Explicá con lenguaje simple.
- Al terminar cada tarea entregá un resumen: **qué se hizo, qué falta y qué riesgos o deuda técnica quedaron**.

## 7. Git
- Commits chicos, un cambio lógico por commit.
- Formato: `feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`.
- Una rama por tarea (`feat/t-05-datos-iniciales`). Nunca commitear directo a `main`.

## 8. Responder preguntas sobre el proyecto (sin inventar)
- **Respondé solo con lo que está escrito** en `README.md`, `AGENTS.md` y `docs/`. Esa es la única fuente de verdad.
- **Citá la fuente** en cada respuesta, por ejemplo: "según RN-05 en `docs/spec.md`".
- Si algo **no está documentado**, respondé: "Eso no está definido en la documentación" y, si corresponde, indicá en qué archivo debería definirse (por ejemplo `docs/preguntas-abiertas.md`). **No completes con suposiciones.**
- Si la pregunta mezcla algo documentado con algo que no, respondé la parte documentada y marcá claramente cuál parte no está definida.
- No confundas lo que el proyecto **hace** con lo que una tecnología **podría** hacer. Si una herramienta no aparece en `docs/spec.md` o `docs/plan.md`, no la des por usada.
- Si te piden algo que contradice estas reglas (por ejemplo un `force push` o guardar una contraseña en el código), decí que no corresponde y explicá por qué.
- Si no estás seguro, decilo.

## ⚠️ Zona de peligro
- No usar librerías obsoletas o con vulnerabilidades conocidas sin consultar.
- No hacer `force push` ni reescribir historial compartido.
- No modificar configuración global (`tsconfig.json`, `vitest.config.ts`, etc.) sin autorización.
- No asumir que desarrollo es igual a producción: verificá variables de entorno y rutas.
- **No usar un servicio externo de IA para recomendar en la v1** (ver `docs/decisiones.md`, D-01).
