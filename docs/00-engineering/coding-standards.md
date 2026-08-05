---
Document ID: ENG-003
Title: Coding Standards
Version: 1.0.0
Status: Draft
Owner: HomeCapital Team
Author: Andres Fonseca
Reviewer: Software Architect
Created: 2026-08-04
Last Updated: 2026-08-04
Related Sprint: Sprint 0.5
Related Issue: HC-002
Category: Engineering
---

# Coding Standards

> Este documento define los estándares de codificación para HomeCapital. Su propósito es garantizar consistencia, legibilidad, mantenibilidad y calidad en todo el código fuente del proyecto.

---

# Objetivos

Los estándares de codificación tienen como finalidad:

- Garantizar un estilo uniforme.
- Facilitar el mantenimiento.
- Reducir errores.
- Mejorar la legibilidad.
- Favorecer el trabajo colaborativo.
- Facilitar las revisiones de código.

---

# Tecnologías

| Tecnología | Versión |
|------------|----------|
| PHP | 8.4+ |
| Laravel | 12.x |
| Vue | 3 |
| TypeScript | 5.x |
| PostgreSQL | 17 |
| Tailwind CSS | 4 |
| Vite | Última estable |

---

# Principios

Todo el código deberá seguir los siguientes principios:

- SOLID
- DRY (Don't Repeat Yourself)
- KISS (Keep It Simple, Stupid)
- YAGNI (You Aren't Gonna Need It)
- Clean Code
- Clean Architecture
- Domain Driven Design (DDD)
- Composition over Inheritance

---

# Estándares PHP

## Declaraciones

Siempre utilizar:

```php
<?php

declare(strict_types=1);
```

---

## Tipado

Siempre utilizar tipado fuerte.

Correcto:

```php
public function create(UserData $data): User
```

Incorrecto:

```php
public function create($data)
```

---

## Propiedades

Siempre tipadas.

```php
private string $name;

private bool $active;
```

---

## Constructor

Promoción de propiedades cuando sea posible.

```php
public function __construct(
    private readonly UserRepository $repository
) {}
```

---

## Clases

Una clase debe tener una única responsabilidad.

---

## Métodos

Un método debería:

- Tener un único propósito.
- Ser pequeño.
- Tener nombres descriptivos.

Ejemplo:

Correcto

```php
calculateMonthlyBalance()
```

Incorrecto

```php
calc()
```

---

# Convenciones de nombres

## Clases

PascalCase

```text
AccountService

CreateTransactionAction

MonthlyBalanceCalculator
```

---

## Interfaces

Siempre terminarán en Interface.

```text
AccountRepositoryInterface

NotificationSenderInterface
```

---

## Enums

```text
TransactionType

MovementStatus

GoalStatus
```

---

## Traits

Finalizarán con Trait.

```text
HasUuidTrait

HasAuditTrailTrait
```

---

## DTO

Finalizarán con Data.

```text
UserData

TransactionData
```

---

## Requests

```text
StoreAccountRequest

UpdateGoalRequest
```

---

## Resources

```text
TransactionResource

UserResource
```

---

## Policies

```text
TransactionPolicy

AccountPolicy
```

---

# Variables

Siempre usar nombres descriptivos.

Correcto

```php
$monthlyIncome

$currentBalance
```

Incorrecto

```php
$x

$temp

$valor
```

---

# Constantes

Siempre en MAYÚSCULAS.

```php
public const MAX_RETRIES = 3;
```

---

# Comentarios

Solo cuando agreguen valor.

Evitar:

```php
// Incrementa contador

$counter++;
```

Preferir código autoexplicativo.

---

# Formato

Seguiremos PSR-12.

Además:

- Indentación: 4 espacios.
- No usar tabs.
- Línea máxima recomendada: 120 caracteres.

---

# Laravel

## Controladores

Solo coordinan la petición.

No contienen lógica de negocio.

---

## Services

Toda la lógica compleja vive aquí.

---

## Actions

Una acción = un caso de uso.

Ejemplo

```text
CreateAccountAction

ImportTransactionsAction

CloseBudgetAction
```

---

## Repositories

Solo acceso a datos.

Nunca reglas de negocio.

---

## Models

Representan entidades.

Evitar lógica compleja.

---

## Validaciones

Siempre mediante FormRequest.

Nunca validar directamente en el controlador.

---

# TypeScript

Siempre activar:

- strict
- noImplicitAny
- strictNullChecks

Nunca usar:

```typescript
any
```

Cuando sea posible utilizar:

```typescript
unknown
```

---

# Vue

Usar siempre:

Composition API

```vue
<script setup lang="ts">
```

Evitar Options API en código nuevo.

---

# PostgreSQL

- snake_case para tablas y columnas.
- Claves primarias llamadas `id`.
- Claves foráneas `<tabla>_id`.
- Índices con nombres descriptivos.

Ejemplo:

```text
idx_transactions_account_id
```

---

# Estructura de carpetas

Seguir siempre la arquitectura definida por el proyecto.

No crear carpetas nuevas sin una ADR o una decisión técnica aprobada.

---

# Dependencias

Antes de incorporar una nueva librería se deberá evaluar:

- Mantenimiento.
- Comunidad.
- Licencia.
- Seguridad.
- Compatibilidad.
- Alternativas.

---

# Prohibiciones

No está permitido:

- Código duplicado.
- Métodos enormes.
- Clases gigantes.
- Variables ambiguas.
- Código comentado.
- Código muerto.
- Hardcodear valores de configuración.
- Consultas SQL dentro de las vistas.

---

# Checklist antes de hacer Commit

- El código compila.
- No existen errores del linter.
- No existen warnings críticos.
- Se ejecutaron las pruebas correspondientes.
- La documentación fue actualizada cuando aplica.

---

# Referencias

- PSR-12
- Laravel Documentation
- PHP-FIG
- Clean Code
- Clean Architecture

---

# Historial

| Versión | Fecha | Descripción |
|----------|-------|-------------|
| 1.0.0 | 2026-08-04 | Creación del documento |
