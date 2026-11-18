# StreamFlix — Especificación (SPEC)

> Cada punto lleva su origen entre corchetes (ver leyenda en `README.md`). Lo marcado **[PROPUESTA]** no viene de tus TPs: revisalo y decidí.

## Objetivo general **[TP3]**
Aplicación web con backend propio que permita consultar un catálogo, registrar lo que el usuario mira y califica, y obtener recomendaciones personalizadas.

## Usuario objetivo **[TP3]**
Personas que usan la plataforma y quieren encontrar contenido que les guste sin revisar cientos de títulos.

## Entidades
Las cinco entidades salen de **[TP4]**. Los campos marcados como propuesta no están en tus TPs.

| Entidad | Campos | Origen |
|---|---|---|
| Usuario | nombre, géneros preferidos | [TP4] |
| | id, email (único), passwordHash, creadoEn | [PROPUESTA] |
| | fechaNacimiento | [PROPUESTA] (para filtrar por edad; [TP3] habla de edad, país e idioma) |
| Contenido | título, géneros, director, actores, duración, sinopsis | [TP4] |
| | id, tipo (película/serie) | [PROPUESTA] |
| | clasificacionEdad, popularidad | [PROPUESTA] (necesarios para filtrar por edad y recomendar populares, que sí están en [TP3]) |
| Historial | qué contenido vio cada usuario | [TP4] |
| | progresoPct | [PROPUESTA] ([TP3] menciona tiempo de reproducción) |
| Calificacion | valoración de un usuario sobre un contenido | [TP4] |
| | puntaje 1–5 | [PROPUESTA] |
| Recomendacion | contenido recomendado a un usuario | [TP4] |
| | motivo, generadaEn | [PROPUESTA] |

## Reglas de negocio (RN)
| Regla | Origen |
|---|---|
| **RN-01** El email es único. La contraseña se guarda con bcrypt, nunca en texto plano. | [PROPUESTA] (bcrypt aparece en [TP1]) |
| **RN-02** Un usuario solo puede ver y modificar sus propios datos, historial y calificaciones. | [TP4] ("solamente puede modificar sus propios datos"); extendida a historial y calificaciones: [PROPUESTA] |
| **RN-03** Una calificación está asociada a un usuario y a un contenido. | [TP4] |
| **RN-03b** Vale de 1 a 5 y hay una sola por usuario y contenido (si vuelve a calificar, se actualiza). | [PROPUESTA] |
| **RN-04** Las recomendaciones deben ser compatibles con las preferencias del usuario y con su edad. | [TP4] (preferencias y configuración) + [TP3] (filtra por edad) |
| **RN-05** Si el usuario no tiene historial, se recomiendan los más populares. | [TP3] y [TP4] |
| **RN-06** Si una búsqueda no encuentra resultados, se ofrecen alternativas del mismo género. | [TP3] y [TP4] ("similares"); "del mismo género" es [PROPUESTA] |
| **RN-07** No se recomienda contenido que el usuario ya vio. | [PROPUESTA] |
| **RN-08** Registrar contenido visto actualiza el historial. | [TP4] |
| **RN-08b** El progreso va de 0 a 100 %. | [PROPUESTA] |
| **RN-09** Secretos y credenciales solo en variables de entorno. | [AGENTS] |
| **RN-10** Las rutas privadas exigen un JWT válido. | [PROPUESTA] (JWT aparece en [TP1]) |

## Historias de usuario (HU)
| Historia | Origen |
|---|---|
| **HU-01** Como visitante quiero registrarme e iniciar sesión. | [TP4] |
| **HU-02** Como usuario quiero ver el catálogo. | [TP4] (consultar películas y series) |
| **HU-03** Como usuario quiero buscar por nombre. | [TP4] |
| **HU-04** Como usuario quiero ver el detalle de una película o serie. | [TP4] |
| **HU-05** Como usuario quiero que se registre lo que miro. | [TP4] |
| **HU-06** Como usuario quiero calificar contenido. | [TP4] |
| **HU-07** Como usuario quiero recibir recomendaciones personalizadas. | [TP4] |
| **HU-08** Como usuario quiero editar mis géneros preferidos. | [TP4] (actualizar preferencias) |
| **HU-09** Como equipo de catálogo quiero cargar contenido nuevo. | [PROPUESTA] (el actor sale de [TP3], pero la funcionalidad no está en [TP4]) |

## Restricciones
| Restricción | Origen |
|---|---|
| Sin IA externa en la v1. | [TP4] |
| Sin notificaciones en la v1. | [TP3] (figuran como mejora futura) |
| Requiere conexión a Internet. | [PROPUESTA] (copiada de [TP1]) |
| Interfaz responsive. | [PROPUESTA] (de [TP1]) |

## Tecnologías
**Ninguna de estas fue elegida por vos para StreamFlix.** Vienen de otros TPs o del ejemplo. Decidí si las mantenés.

| Capa | Tecnología | Origen |
|---|---|---|
| Frontend | React | [TP3] (React o Vue.js) y [TP1] |
| Frontend | Vite | [TP1] |
| Backend | Node.js + Express | [TP1] |
| Backend | TypeScript | [CAPTURA] (usa `tsconfig.json`) y [AGENTS] (recomienda tipado) |
| Base de datos | PostgreSQL | [TP3] (PostgreSQL o MongoDB) y [TP1] |
| ORM | Prisma | [TP1] |
| Autenticación | JWT + bcrypt | [TP1] |
| Tests | Vitest | [CAPTURA] (usa `vitest.config.ts`) |

## API (endpoints) — todos **[TP4]**
| Método | Ruta | Función | Privada |
|---|---|---|---|
| POST | /api/usuarios | Registrar usuario | No |
| POST | /api/login | Iniciar sesión | No |
| PUT | /api/usuarios/:id | Actualizar datos y preferencias | Sí |
| GET | /api/peliculas | Listar catálogo | Sí |
| GET | /api/peliculas/:id | Detalle de contenido | Sí |
| GET | /api/buscar?nombre= | Buscar contenido | Sí |
| POST | /api/usuarios/:id/historial | Registrar contenido visto | Sí |
| POST | /api/usuarios/:id/calificaciones | Registrar calificación | Sí |
| GET | /api/usuarios/:id/recomendaciones | Obtener recomendaciones | Sí |

La columna "Privada" es **[PROPUESTA]** (relacionada con RN-10). Tu TP N4 define las rutas pero no cuáles requieren sesión.
