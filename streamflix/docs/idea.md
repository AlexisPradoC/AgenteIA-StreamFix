# StreamFlix — Idea del cliente

Somos una plataforma de películas y series. Nuestro catálogo es enorme y a los usuarios les cuesta decidir qué ver: pierden tiempo buscando, se frustran y muchos dejan de entrar. Además, mucho contenido no llega a las personas que lo disfrutarían. Queremos un sistema web que le recomiende a cada usuario lo que probablemente le guste.

## Contenido

- Hay **películas y series**.
- De cada una guardamos: género, director, actores, duración y sinopsis.
- Cada contenido tiene una clasificación de edad, para no mostrar a un usuario algo que no corresponde a su edad.

## Usuarios

- **Usuarios:** miran contenido, lo califican y reciben recomendaciones.
- **Administradores:** supervisan que el sistema funcione.
- **Equipo de catálogo:** carga y mantiene las películas y series.
- Cada usuario tiene su perfil, donde puede elegir sus géneros preferidos.

## Qué recomendamos

- Las recomendaciones se basan en lo que el usuario ya vio, cómo lo calificó y sus géneros preferidos.
- Las recomendaciones tienen que ser compatibles con la edad del usuario.
- Si el usuario es nuevo y todavía no vio nada, le mostramos lo más popular o las tendencias.
- Si busca algo que no existe en el catálogo, le ofrecemos alternativas parecidas.
- Las recomendaciones se muestran organizadas, por ejemplo: "Top para ti", "Porque viste…" y "Tendencias".

## Historial y calificaciones

- Queremos registrar qué contenido vio cada usuario.
- Los usuarios pueden calificar lo que vieron.
- Cada vez que un usuario mira, pausa, abandona o califica algo, esa información se guarda para mejorar sus recomendaciones futuras.

## Cuándo se generan las recomendaciones

- Cuando el usuario inicia sesión.
- Cuando termina de ver una película o serie.
- Cuando realiza una búsqueda.
- Cuando modifica su perfil.

## Qué datos puede usar el sistema

- Historial y calificaciones.
- Géneros preferidos.
- Datos del contenido (género, director, actores, duración y sinopsis).
- Información del contexto, como el horario o el dispositivo.

## Cómo sabremos que funciona

- Cuántos usuarios hacen clic en las recomendaciones.
- Cuánto tiempo pasan viendo contenido.
- Si disminuye la cantidad de usuarios que abandonan la plataforma.
- Qué tan satisfechos están, según encuestas.

## Primera versión

**Sí queremos:**
- Registro e inicio de sesión.
- Ver el catálogo, buscar y ver el detalle de cada contenido.
- Registrar lo que se mira y las calificaciones.
- Recomendaciones simples basadas en géneros e historial.

**Todavía no:**
- Una IA externa para recomendar (se evalúa más adelante, cuando haya más usuarios y datos).
- Recomendaciones según amigos, estado de ánimo o por voz.
- Notificaciones de estrenos.
- Reproducción real de video.

## Origen de la información

- Problema, usuarios, disparadores, datos, métricas y mejoras futuras que quedan fuera de la v1: **[TP3]**.
- Contenido, perfil con géneros preferidos, historial, calificaciones, reglas de recomendación y alcance de la v1: **[TP4]**.
- La frase de la clasificación de edad sale de **[TP3]** (filtra contenido no adecuado para su edad); los valores concretos no están definidos.
- Las secciones "Top para ti", "Porque viste…" y "Tendencias": **[TP3]**.

## Pendiente de definir

Hay datos que el cliente todavía no definió, como las clasificaciones de edad concretas, cuántos géneros se pueden elegir o qué significa "popular". Están en `preguntas-abiertas.md`.
