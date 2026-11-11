# Guía de Convenciones de API REST

## 1. Estructura de Rutas y Naming
* **Prefijo Global:** `/api/v1`
* **Formato de Rutas:** Sustantivos en plural, en minúsculas y estilo `kebab-case` (ej. `/api/v1/user-projects`, `/api/v1/kanban-tasks`).
* **Recursos Anidados:** Para representar relaciones directas se usan subrecursos (ej. miembros de un proyecto: `/api/v1/projects/{id}/members`).
* **Comandos y Acciones RPC:** Operaciones que no son CRUD estándar se modelan como comandos:
  * `POST /api/v1/invitations/{token}/accept`
  * `PUT /api/v1/tasks/{id}/move`
  * `POST /api/v1/messages/{id}/convert-to-task`

## 2. Serialización JSON y Mapeo con Base de Datos
* **Payloads y Respuestas:** Estilo `snake_case` (ej. `created_at`, `assignee_id`, `user_id`).
* **Mapeo en Backend:** El contrato expone campos en inglés (`snake_case`), mapeándolos contra el modelo de Prisma mediante el decorador `@map("nombre_columna_espanol")`.

## 3. Seguridad, Roles y Prevención de Descubrimiento
* **Cabecera de Autenticación:** `Authorization: Bearer <jwt_token>` en todas las rutas protegidas.
* **Expiración de Sesión:** El token expira tras 30 minutos de inactividad (HU-03).
* **Control de Acceso (RBAC):** Validación de jerarquía de roles (`ADMINISTRADOR`, `MANAGER`, `USUARIO`) mediante middlewares.
* **Prevención de Enumeración:** Ante un intento de acceso a un proyecto o recurso existente por parte de un usuario no miembro, la API devuelve `404 Not Found` en lugar de `403 Forbidden` para no revelar la existencia del recurso.

## 4. Paginación, Ordenación y Filtros
* **Paginación Estándar (`page`/`limit`):** Aplicada a tareas, archivos, usuarios y notificaciones.
* **Paginación por Cursor (Historial de Chats):** Aplicada en `/api/v1/channels/{id}/messages` mediante `?cursor=uuid&limit=20`.
* **Filtros y Ordenación:**
  * Filtros: `?status=IN_PROGRESS&assignee_id=uuid`
  * Ordenación: `?sort=-created_at` (`-` indica orden descendente).
