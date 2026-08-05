---
Document ID: TEST-001
Title: Testing Strategy
Version: 1.0.0
Status: Draft
Owner: HomeCapital Team
Author: Andres Fonseca
Reviewer: Software Architect
Created: 2026-08-04
Last Updated: 2026-08-04
Related Sprint: Sprint 0.5
Related Issue: HC-008
Category: Testing
---

# Testing Strategy

> Este documento define la estrategia oficial de pruebas para HomeCapital, estableciendo los niveles de testing, herramientas, responsabilidades y criterios de calidad.

---

# Objetivo

Garantizar que cada cambio incorporado al proyecto sea validado de forma automática y reproducible antes de integrarse en la rama principal.

Los objetivos son:

- Detectar errores tempranamente.
- Evitar regresiones.
- Facilitar refactorizaciones.
- Incrementar la confianza en el código.
- Mantener una alta calidad del software.

---

# Pirámide de Testing

HomeCapital seguirá el modelo clásico de la Pirámide de Testing.

```text
                E2E
           ─────────────
           Integration
      ─────────────────────
            Unit Tests
────────────────────────────────
```

La mayor parte de las pruebas deberán ser Unit Tests.

---

# Tipos de pruebas

## Unit Tests

Validan una única unidad de negocio de forma aislada.

Ejemplos:

- Actions
- Services
- Value Objects
- Domain Rules
- Helpers

Características:

- Muy rápidas.
- Sin acceso a base de datos.
- Sin acceso a APIs externas.

---

## Feature Tests

Validan el comportamiento de Laravel.

Ejemplos:

- Requests
- Controllers
- Policies
- Middleware
- Authentication
- Authorization

---

## Integration Tests

Validan la interacción entre módulos.

Ejemplos:

- Service + Repository
- API + Database
- Queue + Events

---

## End-to-End Tests

Simulan el comportamiento de un usuario real.

Ejemplos:

- Login
- Registro
- Crear presupuesto
- Registrar gasto
- Generar reporte

---

# Herramientas

| Herramienta | Uso |
|-------------|-----|
| PestPHP | Unit & Feature Tests |
| PHPUnit | Motor de pruebas |
| Laravel Test Helpers | Testing Laravel |
| Faker | Datos ficticios |
| Mockery | Mocking |
| Vitest | Frontend |
| Playwright | End-to-End |

---

# Organización

```text
tests/
│
├── Unit/
├── Feature/
├── Integration/
├── E2E/
├── Fixtures/
├── Helpers/
└── Traits/
```

---

# Cobertura

Objetivo inicial:

| Tipo | Cobertura mínima |
|-------|-----------------:|
| Domain | 95% |
| Services | 90% |
| Actions | 90% |
| Repositories | 80% |
| Controllers | 70% |
| Policies | 90% |
| Requests | 90% |
| Frontend | 80% |

> La cobertura es un indicador, no un objetivo en sí mismo. Se priorizarán pruebas útiles frente a porcentajes artificialmente altos.

---

# Datos de prueba

Se utilizarán:

- Factories
- Seeders específicos para testing
- Faker
- Base de datos aislada para pruebas

Nunca se utilizarán datos reales.

---

# Convenciones

## Nombres

```php
it_creates_a_new_account()

it_cannot_register_duplicate_email()

it_calculates_monthly_balance_correctly()
```

---

## Estructura AAA

Todas las pruebas seguirán el patrón:

- Arrange
- Act
- Assert

---

# Mocking

Se utilizará Mockery cuando sea necesario aislar dependencias externas.

No abusar de los mocks.

---

# CI/CD

Todas las Pull Requests deberán ejecutar automáticamente:

- PHPStan
- Pint
- Pest
- Vitest
- Cobertura de código (cuando aplique)

Un Pull Request no podrá integrarse si falla cualquiera de estas verificaciones.

---

# Criterios de aceptación

Una funcionalidad se considera correctamente probada cuando:

- Las pruebas relevantes pasan.
- No rompe pruebas existentes.
- Mantiene la cobertura objetivo.
- Valida los escenarios positivos y negativos.

---

# Aplicación práctica en HomeCapital

Ejemplos:

**Crear una cuenta bancaria**

Debe incluir:

- Unit Test del Action.
- Feature Test del endpoint.
- Validación de permisos.
- Validación de reglas de negocio.

---

**Registrar un movimiento**

Debe probar:

- Cálculo del saldo.
- Persistencia.
- Validaciones.
- Eventos generados.

---

# Roadmap de Testing

Sprint 1

- PestPHP
- PHPUnit
- Factories

Sprint 2

- Cobertura

Sprint 3

- Vitest

Sprint 4

- Playwright

Sprint 5

- Automatización completa en GitHub Actions

---

# Referencias

- PestPHP
- PHPUnit
- Laravel Testing
- Playwright
- Vitest

---

# Historial

| Versión | Fecha | Descripción |
|----------|-------|-------------|
| 1.0.0 | 2026-08-04 | Creación del documento |
