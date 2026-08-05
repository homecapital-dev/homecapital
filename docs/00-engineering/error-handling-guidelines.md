---
Document ID: ENG-010
Title: Error Handling Guidelines
Version: 1.0.0
Status: Draft
Owner: HomeCapital Team
Author: Andres Fonseca
Reviewer: Software Architect
Created: 2026-08-04
Last Updated: 2026-08-04
Related Sprint: Sprint 0.5
Related Issue: HC-010
Category: Engineering
---

# Guía de Manejo de Errores

> Este documento define los lineamientos oficiales para el manejo de errores y excepciones en HomeCapital. Su objetivo es garantizar consistencia, trazabilidad y una experiencia de usuario adecuada ante cualquier fallo del sistema.

---

# Objetivos

El manejo de errores debe permitir:

- Detectar fallos rápidamente.
- Facilitar el diagnóstico.
- Evitar pérdida de información.
- Mantener la estabilidad del sistema.
- Proporcionar mensajes claros al usuario.
- Registrar información útil para depuración.

---

# Principios

Todo manejo de errores debe cumplir los siguientes principios:

- Los errores nunca deben ignorarse.
- Todo error debe registrarse.
- El usuario nunca debe recibir información sensible.
- Los mensajes deben ser claros y comprensibles.
- Las excepciones deben manejarse en el nivel adecuado.
- Los errores deben ser consistentes en toda la aplicación.

---

# Clasificación de errores

## Errores de validación

Se producen cuando la información enviada por el usuario no cumple las reglas del sistema.

Ejemplos:

- Campo obligatorio vacío.
- Correo electrónico inválido.
- Valor fuera del rango permitido.

Respuesta:

```
HTTP 422
```

---

## Errores de autenticación

El usuario no ha iniciado sesión o el token es inválido.

Respuesta:

```
HTTP 401
```

---

## Errores de autorización

El usuario está autenticado, pero no posee permisos suficientes.

Respuesta:

```
HTTP 403
```

---

## Recurso inexistente

Cuando el recurso solicitado no existe.

Respuesta:

```
HTTP 404
```

---

## Conflictos

Cuando una operación no puede realizarse debido al estado actual del recurso.

Ejemplos:

- Cuenta bancaria duplicada.
- Presupuesto ya existente.

Respuesta:

```
HTTP 409
```

---

## Error interno

Errores inesperados del sistema.

Ejemplos:

- Excepción no controlada.
- Error de base de datos.
- Servicio externo no disponible.

Respuesta:

```
HTTP 500
```

---

# Estructura estándar de respuestas

Todas las respuestas de error deberán seguir el mismo formato.

```json
{
    "success": false,
    "message": "No fue posible completar la operación.",
    "error": {
        "code": "ACCOUNT_NOT_FOUND",
        "details": null
    },
    "timestamp": "2026-08-04T18:00:00Z",
    "requestId": "req_123456789"
}
```

---

# Códigos internos

Además del código HTTP, HomeCapital utilizará códigos internos.

Ejemplos:

```
AUTH_INVALID_CREDENTIALS

ACCOUNT_NOT_FOUND

TRANSACTION_NOT_ALLOWED

BUDGET_ALREADY_EXISTS

VALIDATION_ERROR

INTERNAL_SERVER_ERROR
```

Estos códigos facilitarán la trazabilidad y el soporte.

---

# Excepciones personalizadas

Siempre que represente una regla de negocio, se deberán utilizar excepciones personalizadas.

Ejemplos:

```php
InsufficientFundsException

BudgetExceededException

DuplicateAccountException

CategoryNotFoundException
```

Evitar lanzar excepciones genéricas cuando exista una alternativa específica.

---

# Registro de errores (Logging)

Todo error deberá registrarse mediante el sistema de logging configurado.

La información registrada deberá incluir:

- Fecha y hora.
- Nivel de severidad.
- Usuario autenticado (si existe).
- Request ID.
- Ruta.
- Método HTTP.
- Mensaje de error.
- Stack Trace (solo en desarrollo).

Nunca registrar:

- Contraseñas.
- Tokens.
- Datos financieros sensibles.
- Información personal innecesaria.

---

# Niveles de Log

| Nivel | Uso |
|--------|-----|
| DEBUG | Información para desarrollo |
| INFO | Eventos importantes |
| NOTICE | Comportamientos esperados relevantes |
| WARNING | Situaciones anómalas recuperables |
| ERROR | Error funcional |
| CRITICAL | Falla grave |
| ALERT | Servicio comprometido |
| EMERGENCY | Sistema inutilizable |

---

# Manejo de excepciones

Se recomienda capturar únicamente las excepciones que puedan gestionarse.

Incorrecto:

```php
try {
    //
} catch (Exception $e) {
}
```

Correcto:

```php
try {
    //
} catch (BudgetExceededException $e) {
    //
}
```

Las excepciones no recuperables deberán propagarse hasta el manejador global.

---

# Mensajes para el usuario

Los mensajes deben:

- Ser claros.
- Evitar lenguaje técnico.
- Indicar qué ocurrió.
- Sugerir una acción cuando sea posible.

Correcto:

```
No fue posible guardar el presupuesto. Inténtalo nuevamente.
```

Incorrecto:

```
SQLSTATE[23505]: Duplicate key...
```

---

# Integración con Laravel

HomeCapital utilizará el manejador global de excepciones de Laravel para:

- Transformar excepciones en respuestas JSON.
- Registrar eventos.
- Ocultar detalles internos en producción.

Las excepciones de negocio deberán implementarse en:

```
app/Exceptions/
```

---

# Integración con Frontend

El frontend deberá:

- Mostrar mensajes amigables.
- Diferenciar errores de validación y errores del servidor.
- Permitir reintentos cuando sea posible.
- Registrar errores críticos mediante herramientas de monitoreo (cuando se implementen).

---

# Aplicación práctica en HomeCapital

## Crear una cuenta bancaria

Si el nombre ya existe:

- Lanzar `DuplicateAccountException`.
- Registrar un WARNING.
- Responder HTTP 409.

---

## Registrar un gasto

Si el presupuesto fue excedido:

- Lanzar `BudgetExceededException`.
- Registrar un WARNING.
- Mostrar un mensaje claro al usuario.

---

## Error de base de datos

- Registrar ERROR.
- Devolver HTTP 500.
- No exponer información interna.

---

# Checklist

Antes de aprobar una funcionalidad verificar:

- [ ] Todas las excepciones están controladas.
- [ ] Se utilizan códigos HTTP correctos.
- [ ] Los mensajes son comprensibles.
- [ ] Se registran los errores.
- [ ] No se exponen datos sensibles.
- [ ] Existen excepciones específicas cuando aplica.

---

# Referencias

- Laravel Exception Handling
- PSR-3 Logger Interface
- RFC 9110 HTTP Semantics
- OWASP Error Handling Cheat Sheet

---

# Historial

| Versión | Fecha | Descripción |
|----------|-------|-------------|
| 1.0.0 | 2026-08-04 | Creación del documento |
