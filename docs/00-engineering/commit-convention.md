---
Document ID: ENG-006
Title: Commit Convention
Version: 1.0.0
Status: Draft
Owner: HomeCapital Team
Author: Andres Fonseca
Reviewer: Software Architect
Created: 2026-08-04
Last Updated: 2026-08-04
Related Sprint: Sprint 0.5
Related Issue: HC-005
Category: Engineering
---

# Commit Convention

> Este documento define la política oficial para la creación de commits en HomeCapital. Su objetivo es mantener un historial claro, consistente y trazable.

---

# Objetivos

La política de commits busca:

- Mantener un historial legible.
- Facilitar auditorías.
- Mejorar el seguimiento de cambios.
- Simplificar la generación del CHANGELOG.
- Relacionar cada cambio con una Issue.

---

# Estándar adoptado

HomeCapital adopta **Conventional Commits 1.0.0** con algunas reglas adicionales propias del proyecto.

Formato:

```
<type>(<scope>): <description> (HC-XXX)
```

Ejemplo:

```
feat(accounts): implement account creation (HC-021)

docs(engineering): define coding standards (HC-002)

fix(auth): resolve login validation (HC-034)
```

---

# Tipos permitidos

| Tipo | Uso |
|------|-----|
| feat | Nueva funcionalidad |
| fix | Corrección de errores |
| docs | Documentación |
| refactor | Refactorización sin cambios funcionales |
| test | Pruebas |
| chore | Mantenimiento |
| style | Cambios de formato |
| perf | Mejoras de rendimiento |
| build | Build y dependencias |
| ci | Integración continua |
| revert | Revertir cambios |

---

# Scopes

El scope identifica el módulo afectado.

Ejemplos:

```
accounts
transactions
budgets
dashboard
reports
notifications
auth
database
engineering
architecture
testing
api
frontend
backend
```

---

# Reglas generales

Todo commit debe:

- Tener un único propósito.
- Estar asociado a una Issue.
- Ser pequeño y fácil de revisar.
- Compilar correctamente.
- No romper el proyecto.

---

# Cuándo hacer un commit

Se recomienda hacer un commit cuando:

- Se completa una funcionalidad.
- Se termina una sección de documentación.
- Se finaliza una migración.
- Se implementa una prueba.
- Se corrige un error específico.

---

# Cuándo NO hacer un commit

Evitar commits cuando:

- El proyecto no compila.
- Existen archivos temporales.
- El trabajo está incompleto.
- Hay código comentado.
- Existen errores conocidos sin documentar.

---

# Ejemplos válidos

## Nueva funcionalidad

```
feat(accounts): create account module (HC-012)
```

## Corrección

```
fix(api): resolve transaction validation (HC-031)
```

## Documentación

```
docs(engineering): define git workflow (HC-003)
```

## Refactor

```
refactor(transactions): simplify balance calculation (HC-041)
```

## Testing

```
test(accounts): add account service tests (HC-054)
```

---

# Ejemplos NO permitidos

```
Cambios
```

```
Update
```

```
Correcciones
```

```
asd
```

```
últimos cambios
```

```
fix
```

---

# Tamaño de los commits

Preferir commits pequeños.

Ideal:

- 1 objetivo.
- 5 a 20 archivos.

Evitar:

- 100 archivos modificados.
- Varias funcionalidades en un mismo commit.

---

# Frecuencia

Se recomienda realizar varios commits durante una sesión de trabajo.

Es preferible:

5 commits pequeños

que

1 commit enorme.

---

# Relación con GitHub

Cada commit deberá estar relacionado con:

- Una Issue.
- Un Pull Request.
- Un Sprint.

---

# Versionado

Los commits deberán permitir generar automáticamente el CHANGELOG del proyecto.

---

# Buenas prácticas

- Escribir mensajes en inglés.
- Usar verbo en presente.
- Ser específico.
- No utilizar abreviaturas ambiguas.
- Mantener consistencia.

---

# Prohibiciones

No está permitido:

- Commits sin descripción.
- Commits con múltiples objetivos.
- Commits sobre `main`.
- Reescribir el historial compartido.
- Eliminar información del historial.

---

# Checklist antes del commit

- Código compilando.
- Linter sin errores.
- Pruebas ejecutadas (cuando apliquen).
- Documentación actualizada.
- Issue asociada.
- Mensaje siguiendo Conventional Commits.

---

# Referencias

- Conventional Commits
- Semantic Versioning
- Git Documentation

---

# Historial

| Versión | Fecha | Descripción |
|----------|-------|-------------|
| 1.0.0 | 2026-08-04 | Creación del documento |
