---
Document ID: DEVOPS-002
Title: CI/CD Strategy
Version: 1.0.0
Status: Draft
Owner: HomeCapital Team
Author: Andres Fonseca
Reviewer: Software Architect
Created: 2026-08-04
Last Updated: 2026-08-04
Related Sprint: Sprint 0.5
Related Issue: HC-013
Category: DevOps
---

# Estrategia de Integración Continua y Despliegue Continuo (CI/CD)

> Este documento define la estrategia de Integración Continua (CI) y Despliegue Continuo (CD) para HomeCapital, estableciendo el flujo de trabajo desde el desarrollo local hasta la publicación en producción.

---

# Objetivos

La estrategia CI/CD busca:

- Automatizar la validación del código.
- Detectar errores lo antes posible.
- Mantener la rama principal estable.
- Reducir el riesgo en los despliegues.
- Garantizar una calidad consistente.
- Facilitar futuras entregas continuas.

---

# Principios

Toda integración deberá cumplir:

- Automatización antes que procesos manuales.
- La rama `main` siempre debe estar estable.
- Ningún cambio llega a `main` sin revisión.
- Todo Pull Request ejecuta validaciones automáticas.
- Los despliegues deben ser repetibles.

---

# Flujo de desarrollo

```text
Issue
   │
Feature Branch
   │
Desarrollo local
   │
Commit
   │
Push
   │
Pull Request
   │
GitHub Actions
   │
Revisión
   │
Merge
   │
Release
```

---

# Entornos

## Development

Uso diario por los desarrolladores.

Características:

- APP_DEBUG=true
- Datos de prueba
- Logging detallado

---

## Staging

Replica el entorno de producción.

Características:

- Pruebas funcionales.
- Validación antes del despliegue.
- Datos anonimizados o ficticios.

---

## Production

Entorno final para usuarios.

Características:

- APP_DEBUG=false
- Logs protegidos
- HTTPS obligatorio
- Monitoreo activo

---

# Pipeline de Integración Continua

Cada Pull Request deberá ejecutar:

1. Instalación de dependencias.
2. Validación de sintaxis.
3. PHP CS Fixer / Laravel Pint.
4. PHPStan.
5. Pest / PHPUnit.
6. Vitest (Frontend).
7. Construcción de Vite.
8. Verificación de cobertura (cuando aplique).

Si cualquiera de estas etapas falla, el Pull Request no podrá fusionarse.

---

# Pipeline de Despliegue

Inicialmente el despliegue será manual.

En futuras fases podrá automatizarse.

Flujo previsto:

```text
Merge a main
      │
Crear Release
      │
Generar artefacto
      │
Desplegar Staging
      │
Validación
      │
Desplegar Producción
```

---

# GitHub Actions

Se implementarán workflows independientes.

## Quality

Validará:

- Laravel Pint
- PHPStan
- Pest

---

## Frontend

Validará:

- npm install
- npm run build
- Vitest

---

## Security

Ejecutará:

```bash
composer audit

npm audit
```

---

## Release

En futuras versiones:

- Etiquetado automático.
- Generación de changelog.
- Publicación de releases.

---

# Protección de ramas

La rama `main` deberá tener:

- Pull Request obligatorio.
- Al menos una revisión aprobada.
- Todos los workflows en estado exitoso.
- Sin commits directos.

---

# Estrategia de versiones

Se utilizará Semantic Versioning.

Formato:

```
MAJOR.MINOR.PATCH
```

Ejemplos:

```
1.0.0

1.1.0

1.1.1
```

---

# Estrategia de Releases

Cada release deberá incluir:

- Número de versión.
- Changelog.
- Issues cerradas.
- Breaking Changes (si existen).

---

# Gestión de secretos

Los secretos del pipeline se almacenarán mediante GitHub Secrets.

Ejemplos:

- APP_KEY
- DATABASE_URL
- DEPLOY_TOKEN
- SSH_PRIVATE_KEY

Nunca almacenar secretos en el repositorio.

---

# Calidad mínima

Para aceptar un Pull Request deberán cumplirse:

- Build exitoso.
- Pruebas exitosas.
- PHPStan sin errores.
- Pint sin cambios pendientes.
- Cobertura dentro del objetivo definido.

---

# Integración con HomeCapital

Cuando se implemente el backend:

- Ejecutar pruebas automáticamente.
- Validar estilo de código.
- Construir frontend.
- Generar artefactos listos para despliegue.

---

# Roadmap

Sprint 1

- Configuración inicial de GitHub Actions.

Sprint 2

- Automatización de pruebas.

Sprint 3

- Integración con análisis estático.

Sprint 4

- Automatización de releases.

Sprint 5

- Despliegue automático a Staging.

Sprint 6

- Despliegue automático a Producción.

---

# Checklist

Antes de aprobar un Pull Request verificar:

- [ ] Build exitoso.
- [ ] Pruebas aprobadas.
- [ ] Análisis estático aprobado.
- [ ] Sin conflictos.
- [ ] Revisión completada.
- [ ] Changelog actualizado cuando corresponda.

---

# Referencias

- GitHub Actions
- Laravel Deployment
- Semantic Versioning
- Conventional Commits
- Twelve-Factor App

---

# Historial

| Versión | Fecha | Descripción |
|----------|-------|-------------|
| 1.0.0 | 2026-08-04 | Creación del documento |
