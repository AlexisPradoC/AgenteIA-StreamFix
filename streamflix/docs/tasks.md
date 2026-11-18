# StreamFlix — Tareas

> **Origen general:** la lista de funcionalidades sale de **[TP4]**. El formato de las tareas sale de **[CAPTURA]**. Los criterios "Terminada cuando", los códigos HTTP (400, 401, 403, 409), el orden y las dependencias son **[PROPUESTA]**: revisalos.

Formato: cada tarea tiene estado, agente, qué hacer, RN/HU, dependencias y criterios de "terminada cuando".

## Etapa 1 — Base

### T-01 — Proyecto backend y configuración
- **Origen:** [PROPUESTA] basada en [CAPTURA] (Node, TypeScript, Vitest) y [AGENTS] (credenciales en `.env`).
- **Estado:** [ ]
- **Agente:** Dev backend
- **Qué hacer:** Inicializar el backend con Node, TypeScript, Express y Vitest. Cargar variables de entorno desde `.env`. Crear `.env.example` solo con los nombres.
- **RN / HU:** RN-09
- **Depende de:** ninguna
- **Terminada cuando:**
  1. `npm test` corre y pasa con un test de ejemplo.
  2. Una consulta a `GET /salud` devuelve estado 200.
  3. No hay ningún secreto escrito en el código.

### T-02 — Logger y manejo de errores
- **Origen:** [PROPUESTA] basada en [AGENTS] sección 3 (logs y errores).
- **Estado:** [ ]
- **Agente:** Tester + Dev backend
- **Qué hacer:** Crear un logger con niveles `debug`, `info` y `error`, y un middleware que convierta los errores en respuestas HTTP claras.
- **RN / HU:** RN-09
- **Depende de:** T-01
- **Terminada cuando:**
  1. Un error lanzado en una ruta devuelve un JSON con mensaje claro y el código HTTP correcto.
  2. Con `LOG_LEVEL=info` no se imprimen mensajes `debug`.

### T-03 — Base de datos y modelos
- **Origen:** [TP4] (entidades) + [PROPUESTA] (Prisma y PostgreSQL, de [TP1]).
- **Estado:** [ ]
- **Agente:** Dev backend
- **Qué hacer:** Definir el esquema de Usuario, Contenido, Historial y Calificación en Prisma y la conexión a PostgreSQL.
- **RN / HU:** RN-01, RN-03
- **Depende de:** T-01
- **Terminada cuando:**
  1. La migración se aplica sin errores.
  2. No se puede crear dos usuarios con el mismo email ni dos calificaciones del mismo usuario para el mismo contenido.

## Etapa 2 — Usuarios y seguridad

### T-04 — Registro de usuarios
- **Origen:** [TP4] (registrar usuarios) + [PROPUESTA] (bcrypt, de [TP1]).
- **Estado:** [ ]
- **Agente:** Tester + Dev backend
- **Qué hacer:** Implementar `POST /api/usuarios` con validación de datos y contraseña con bcrypt.
- **RN / HU:** RN-01 · HU-01
- **Depende de:** T-02, T-03
- **Terminada cuando:**
  1. Un registro válido devuelve 201 y no incluye la contraseña en la respuesta.
  2. El hash guardado en la base no coincide con el texto de la contraseña.
  3. Un email repetido devuelve 409 y un email inválido devuelve 400.

### T-05 — Inicio de sesión con JWT
- **Origen:** [TP4] (iniciar sesión) + [PROPUESTA] (JWT, de [TP1]).
- **Estado:** [ ]
- **Agente:** Tester + Dev backend
- **Qué hacer:** Implementar `POST /api/login` y el middleware que valida el JWT.
- **RN / HU:** RN-10 · HU-01
- **Depende de:** T-04
- **Terminada cuando:**
  1. Credenciales correctas devuelven un token válido.
  2. Credenciales incorrectas devuelven 401.
  3. Una ruta privada sin token devuelve 401.

### T-06 — Editar usuario y preferencias
- **Origen:** [TP4] (actualizar preferencias y regla de modificar solo los propios datos).
- **Estado:** [ ]
- **Agente:** Tester + Dev backend
- **Qué hacer:** Implementar `PUT /api/usuarios/:id` para actualizar nombre y géneros preferidos.
- **RN / HU:** RN-02 · HU-08
- **Depende de:** T-05
- **Terminada cuando:**
  1. Un usuario puede actualizar sus propios datos.
  2. Intentar modificar a otro usuario devuelve 403.

## Etapa 3 — Catálogo

### T-07 — Listar y ver detalle de contenido
- **Origen:** [TP4] (consultar películas y ver una película).
- **Estado:** [ ]
- **Agente:** Tester + Dev backend
- **Qué hacer:** Implementar `GET /api/peliculas` y `GET /api/peliculas/:id`, con datos de ejemplo cargados al iniciar.
- **RN / HU:** HU-02, HU-04
- **Depende de:** T-05
- **Terminada cuando:**
  1. El listado devuelve los contenidos de ejemplo.
  2. Un id inexistente devuelve 404.

### T-08 — Búsqueda con alternativas
- **Origen:** [TP3] y [TP4] (buscar y ofrecer alternativas si no existe).
- **Estado:** [ ]
- **Agente:** Tester + Dev backend
- **Qué hacer:** Implementar `GET /api/buscar?nombre=`. Si no hay coincidencias, devolver contenidos del mismo género como alternativas.
- **RN / HU:** RN-06 · HU-03
- **Depende de:** T-07
- **Terminada cuando:**
  1. Buscar un título existente lo devuelve primero.
  2. Buscar un título inexistente devuelve una lista de alternativas marcada como tal.
  3. Una búsqueda vacía devuelve 400.

## Etapa 4 — Historial y calificaciones

### T-09 — Registrar contenido visto
- **Origen:** [TP4] (registrar cuando un usuario mira contenido).
- **Estado:** [ ]
- **Agente:** Tester + Dev backend
- **Qué hacer:** Implementar `POST /api/usuarios/:id/historial` con el progreso de visualización.
- **RN / HU:** RN-02, RN-08 · HU-05
- **Depende de:** T-07
- **Terminada cuando:**
  1. Un progreso de 0 a 100 se guarda en el historial.
  2. Un progreso fuera de rango devuelve 400.
  3. Registrar en el historial de otro usuario devuelve 403.

### T-10 — Registrar calificaciones
- **Origen:** [TP4] (registrar calificaciones) + [PROPUESTA] (rango 1–5 y una por contenido).
- **Estado:** [ ]
- **Agente:** Tester + Dev backend
- **Qué hacer:** Implementar `POST /api/usuarios/:id/calificaciones`.
- **RN / HU:** RN-02, RN-03 · HU-06
- **Depende de:** T-07
- **Terminada cuando:**
  1. Un puntaje de 1 a 5 se guarda.
  2. Calificar de nuevo el mismo contenido actualiza el puntaje, sin crear un segundo registro.
  3. Un puntaje de 0 o 6 devuelve 400.

## Etapa 5 — Recomendaciones

### T-11 — Recomendaciones por géneros e historial
- **Origen:** [TP4] (funcionalidad implementada primero) + [TP3] (filtrar por edad).
- **Estado:** [ ]
- **Agente:** Tester + Dev backend
- **Qué hacer:** Implementar `GET /api/usuarios/:id/recomendaciones` con el algoritmo de `docs/plan.md`.
- **RN / HU:** RN-04, RN-05, RN-07 · HU-07
- **Depende de:** T-09, T-10
- **Terminada cuando:**
  1. Un usuario que ve terror y suspenso recibe contenido de esos géneros.
  2. No se recomienda nada que ya haya visto.
  3. Un usuario sin historial recibe los más populares.
  4. Un menor de edad no recibe contenido con clasificación para mayores.

## Etapa 6 — Frontend

### T-12 — Login y registro en pantalla
- **Origen:** [TP4] (el frontend muestra formularios de inicio de sesión).
- **Estado:** [ ]
- **Agente:** Dev frontend
- **Qué hacer:** Crear pantallas de registro e inicio de sesión conectadas al backend, con estados de carga y error.
- **RN / HU:** HU-01
- **Depende de:** T-05
- **Terminada cuando:**
  1. Un usuario puede registrarse e iniciar sesión desde la interfaz.
  2. Los errores del backend se muestran con un mensaje claro.

### T-13 — Catálogo, búsqueda y recomendaciones en pantalla
- **Origen:** [TP4] (el frontend muestra películas y recomendaciones).
- **Estado:** [ ]
- **Agente:** Dev frontend
- **Qué hacer:** Mostrar el catálogo, el buscador y la sección "Top para ti" con las recomendaciones.
- **RN / HU:** HU-02, HU-03, HU-07
- **Depende de:** T-08, T-11, T-12
- **Terminada cuando:**
  1. La pantalla principal muestra recomendaciones del usuario conectado.
  2. La interfaz se ve bien a 375 px y a 1024 px o más.
