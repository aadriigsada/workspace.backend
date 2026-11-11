# Guía de Gestión de Errores

## Formato Único de Respuesta de Error
Todas las respuestas de fallo (`4xx` y `5xx`) responden con este formato JSON:

```json
{
  "success": false,
  "error": {
    "code": "INVALID_PAYLOAD",
    "message": "Los datos de la petición contienen errores de validación.",
    "details": [
      {
        "field": "email",
        "issue": "El formato del correo electrónico no es válido."
      }
    ],
    "timestamp": "2026-11-11T17:30:00.000Z"
  }
}
Tabla de Códigos de Error MapeadosCódigo HTTPerror.code de DominioDescripción / Caso de Uso400 Bad RequestINVALID_PAYLOADFormato o tipos de datos incorrectos en body/params.400 Bad RequestINVALID_STATUS_TRANSITIONIntento de cambio de estado no permitido según reglas del flujo.401 UnauthorizedUNAUTHORIZEDJWT no enviado, manipulado o expirado (tras 30 min de inactividad).401 UnauthorizedINVITATION_EXPIREDEnlace de invitación caducado o previamente utilizado.403 ForbiddenINSUFFICIENT_PERMISSIONSRol insuficiente para la acción ejecutada.404 Not FoundRESOURCE_NOT_FOUNDRecurso inexistente o no accesible por pertenencia a proyecto.409 ConflictRESOURCE_ALREADY_EXISTSIntento de duplicación de clave única (ej. email registrado).413 Payload Too LargeFILE_TOO_LARGEEl archivo subido excede el límite máximo permitido.415 Unsupported Media TypeUNSUPPORTED_FILE_TYPEExtensión de archivo no permitida en la plataforma.429 Too Many RequestsRATE_LIMIT_EXCEEDEDExceso de peticiones en ventana de tiempo definida.500 Internal Server ErrorINTERNAL_SERVER_ERRORFallo no controlado en el servidor o caída de la base de datos.
---
