# Especificación de eventos WebSockets (Socket.io)

## Handshake y autenticación

Al conectar desde el cliente React, se envía el token JWT en las opciones de autenticación:

```javascript
const socket = io("https://api.empresa.com", {
  auth: {
    token: "Bearer <jwt_token>"
  }
});
```

## Suscripción a salas (rooms)

| Evento | Payload | Descripción |
|---|---|---|
| `join_channel` | `{ channel_id }` | Suscribirse a la sala del canal. |
| `leave_channel` | `{ channel_id }` | Abandonar la sala del canal. |
| `join_board` | `{ project_id }` | Suscribirse a la sala del tablero del proyecto. |

## Catálogo de eventos

| Evento | Emisor | Payload | Descripción |
|---|---|---|---|
| `send_message` | Cliente | `{ channel_id, content, parent_message_id }` | Enviar un mensaje nuevo. |
| `new_message` | Servidor | `{ id, content, user_id, channel_id, created_at }` | Difundir el mensaje a la sala. |
| `typing_start` | Cliente | `{ channel_id }` | Notificar que el usuario empieza a escribir. |
| `user_typing` | Servidor | `{ user_id, channel_id }` | Difundir el indicador de escritura. |
| `task_moved` | Servidor | `{ task_id, project_id, status, column_order }` | Sincronizar el movimiento de una tarea en Kanban. |
| `presence_change` | Servidor | `{ user_id, status }` | Notificar un cambio de presencia (`ONLINE`, `AWAY`, `OFFLINE`). |
