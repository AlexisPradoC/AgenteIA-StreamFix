# StreamFlix — Plan técnico

> Cada sección indica su origen (ver leyenda en `README.md`). Lo marcado **[PROPUESTA]** no viene de tus TPs.

## Arquitectura del backend — **[TP4]**
```
Frontend → Controller → Service → Repository → Base de datos
```
| Capa | Responsabilidad | No debe hacer |
|---|---|---|
| Controller | Recibir la petición, validar formato y devolver la respuesta HTTP | Reglas de negocio ni acceso a la base |
| Service | Aplicar reglas de negocio (RN) | Hablar HTTP ni escribir consultas |
| Repository | Consultar y guardar en la base de datos | Decidir reglas de negocio |

**Por qué [TP4]:** separar responsabilidades hace que cada parte se pueda cambiar y probar por separado.

## Estructura de carpetas (backend)
**[TP4]** define `controllers`, `services`, `repositories`, `models` y `database`. Las carpetas `middlewares` y `config` y los nombres de cada archivo son **[PROPUESTA]**.

```
backend/src/
├── controllers/   usuarioController, peliculaController, historialController,
│                  calificacionController, recomendacionController
├── services/      usuarioService, peliculaService, historialService,
│                  calificacionService, recomendacionService
├── repositories/  usuarioRepository, peliculaRepository, historialRepository,
│                  calificacionRepository
├── models/        tipos de Usuario, Contenido, Historial, Calificacion, Recomendacion
├── middlewares/   autenticacion (JWT), manejoErrores
├── config/        variables de entorno, logger
└── database/      conexión (Prisma)
```

## Algoritmo de recomendación (v1)
Los pasos 1, 3 y 6 salen de **[TP4]** (funcionalidad implementada) y de **[TP3]** (usuarios nuevos reciben populares). Los pasos 2, 4 y 5 (calificaciones, quitar lo ya visto y el orden por afinidad y popularidad) son **[PROPUESTA]**.

1. Obtener el usuario, sus géneros preferidos y su historial.
2. Calcular los géneros más consumidos y mejor calificados.
3. Buscar contenido de esos géneros.
4. Quitar lo ya visto (RN-07) y lo no apto por edad (RN-04).
5. Ordenar por afinidad con los géneros y luego por popularidad.
6. Si no hay historial, devolver los más populares (RN-05).

## Variables de entorno — **[PROPUESTA]** (basada en [AGENTS]: credenciales en `.env`)
`DATABASE_URL`, `JWT_SECRET`, `JWT_EXPIRES_IN`, `PORT`, `LOG_LEVEL`, `ADMIN_EMAIL`, `ADMIN_PASSWORD`.

## Pruebas — **[PROPUESTA]** (basada en [AGENTS] sección 5 y [CAPTURA])
- Unitarias de Service con repositorios simulados (mocks).
- Pruebas de endpoints con casos correcto, inválido y límite.
