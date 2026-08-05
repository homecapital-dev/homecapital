---
Document ID: DEVOPS-001
Title: Logging & Monitoring Guidelines
Version: 1.0.0
Status: Draft
Owner: HomeCapital Team
Author: Andres Fonseca
Reviewer: Software Architect
Created: 2026-08-04
Last Updated: 2026-08-04
Related Sprint: Sprint 0.5
Related Issue: HC-012
Category: DevOps
---

# Guía de Logging y Monitoreo

> Este documento define la estrategia oficial de registro de eventos, auditoría, monitoreo y observabilidad para HomeCapital.

---

# Objetivo

Garantizar que cualquier evento relevante del sistema pueda:

- Ser identificado.
- Ser rastreado.
- Ser auditado.
- Ser monitoreado.
- Facilitar el diagnóstico.
- Reducir el tiempo de resolución de incidentes.

---

# Principios

Todo evento deberá cumplir:

- Ser trazable.
- Tener contexto suficiente.
- Ser consistente.
- No contener información sensible.
- Ser útil para desarrolladores y operadores.

---

# Observabilidad

HomeCapital seguirá los tres pilares de la observabilidad.

## Logs

Registrar eventos importantes.

Ejemplo:

- Inicio de sesión.
- Registro de gastos.
- Cambios de presupuesto.
- Errores.

---

## Métricas

Medir el comportamiento del sistema.

Ejemplos:

- Tiempo de respuesta.
- Número de usuarios.
- Número de movimientos.
- Consumo de memoria.
- Uso de CPU.

---

## Trazas (Tracing)

Permiten seguir una petición desde que entra al sistema hasta que finaliza.

Cada petición tendrá un identificador único.

```
Request ID

req_01HX3A91W8N2
```

---

# Niveles de Logging

| Nivel | Uso |
|--------|-----|
| DEBUG | Información detallada para desarrollo |
| INFO | Eventos normales |
| NOTICE | Eventos importantes esperados |
| WARNING | Situaciones recuperables |
| ERROR | Fallos funcionales |
| CRITICAL | Servicios parcialmente caídos |
| ALERT | Riesgo elevado |
| EMERGENCY | Sistema no disponible |

---

# Eventos que deben registrarse

## Autenticación

Registrar:

- Login exitoso.
- Login fallido.
- Logout.
- Cambio de contraseña.
- Recuperación de contraseña.

---

## Seguridad

Registrar:

- Cambios de permisos.
- Creación de usuarios.
- Eliminación de usuarios.
- Intentos de acceso no autorizado.
- Bloqueos por fuerza bruta.

---

## Operaciones financieras

Registrar:

- Creación de cuentas.
- Eliminación de cuentas.
- Registro de ingresos.
- Registro de gastos.
- Transferencias.
- Ajustes manuales.

---

## Sistema

Registrar:

- Inicio de aplicación.
- Despliegues.
- Errores.
- Excepciones.
- Jobs fallidos.
- Eventos críticos.

---

# Información mínima del log

Todo evento deberá incluir:

- Fecha.
- Hora.
- Nivel.
- Usuario (si existe).
- Request ID.
- Dirección IP.
- Ruta.
- Método HTTP.
- Mensaje.
- Contexto.

---

# Formato recomendado

```json
{
    "timestamp": "2026-08-04T19:20:00Z",
    "level": "INFO",
    "requestId": "req_123456789",
    "userId": 12,
    "route": "/api/accounts",
    "method": "POST",
    "message": "Cuenta creada correctamente",
    "context": {
        "accountId": 34
    }
}
```

---

# Información que nunca debe registrarse

Prohibido registrar:

- Contraseñas.
- Tokens.
- API Keys.
- Secretos.
- Datos bancarios completos.
- Números de tarjetas.
- Información personal sensible.

---

# Request ID

Cada petición recibirá un identificador único.

Ejemplo:

```
req_7b8c12de45
```

El Request ID deberá propagarse durante todo el ciclo de la petición.

---

# Auditoría

Se consideran eventos auditables:

- Inicio de sesión.
- Cierre de sesión.
- Creación de cuentas.
- Eliminación de registros.
- Modificación de presupuestos.
- Exportación de información.
- Cambios de configuración.

---

# Rotación de logs

Los logs deberán:

- Rotarse diariamente.
- Mantenerse por un tiempo definido.
- Comprimirse automáticamente.
- Eliminarse según la política de retención.

Configuración inicial:

- Rotación diaria.
- Retención: 30 días.

---

# Monitoreo

Inicialmente se utilizarán las herramientas nativas de Laravel.

En futuras versiones se integrarán:

- Laravel Pulse.
- Laravel Telescope (solo desarrollo).
- Sentry.
- Grafana.
- Prometheus.
- Loki.
- OpenTelemetry.

---

# Alertas

Deberán generarse alertas cuando:

- Existan múltiples errores consecutivos.
- Se detecten intentos de acceso masivos.
- Fallen procesos críticos.
- El tiempo de respuesta exceda el umbral definido.

---

# Rendimiento

Métricas iniciales:

- Tiempo promedio de respuesta.
- Tiempo máximo.
- Consultas SQL por petición.
- Memoria utilizada.
- Número de errores por minuto.

---

# Integración con Laravel

Se utilizarán:

- Log Facade.
- Monolog.
- Canales de logging.
- Middleware para Request ID.
- Manejador global de excepciones.

---

# Integración con HomeCapital

## Crear un gasto

Registrar:

- Usuario.
- Cuenta.
- Categoría.
- Presupuesto.
- Resultado.

---

## Crear un presupuesto

Registrar:

- Usuario.
- Periodo.
- Categoría.
- Resultado.

---

## Login

Registrar:

- Usuario.
- IP.
- Navegador.
- Resultado.
- Request ID.

---

# Checklist

Antes de aprobar una funcionalidad verificar:

- [ ] Se registran eventos importantes.
- [ ] No existen datos sensibles en logs.
- [ ] Se utiliza Request ID.
- [ ] Los niveles de log son correctos.
- [ ] Los errores generan trazabilidad.
- [ ] Los eventos críticos son auditables.

---

# Roadmap

Sprint 1

- Logging nativo Laravel.

Sprint 2

- Middleware Request ID.

Sprint 3

- Auditoría.

Sprint 4

- Laravel Pulse.

Sprint 5

- OpenTelemetry.

Sprint 6

- Grafana + Loki + Prometheus.

---

# Referencias

- PSR-3 Logger Interface
- Monolog
- Laravel Logging
- Laravel Telescope
- Laravel Pulse
- OpenTelemetry
- Grafana
- Prometheus
- Loki
- OWASP Logging Cheat Sheet

---

# Historial

| Versión | Fecha | Descripción |
|----------|-------|-------------|
| 1.0.0 | 2026-08-04 | Creación del documento |
