---
Document ID: ENG-014
Title: Development Environment Setup
Version: 1.0.0
Status: Draft
Owner: HomeCapital Team
Author: Andres Fonseca
Reviewer: Software Architect
Created: 2026-08-04
Last Updated: 2026-08-04
Related Sprint: Sprint 0.5
Related Issue: HC-014
Category: Engineering
---

# Guía de Configuración del Entorno de Desarrollo

> Este documento describe el entorno oficial de desarrollo para HomeCapital. Su propósito es garantizar que todos los desarrolladores trabajen con las mismas herramientas, versiones y configuraciones para reducir inconsistencias y facilitar la colaboración.

---

# Objetivos

Esta guía busca:

- Estandarizar el entorno de desarrollo.
- Reducir problemas de configuración.
- Facilitar el proceso de incorporación de nuevos desarrolladores.
- Garantizar compatibilidad entre herramientas.
- Simplificar la resolución de problemas.

---

# Requisitos de Hardware

Mínimos recomendados:

| Recurso | Recomendado |
|----------|------------:|
| CPU | 4 núcleos |
| RAM | 16 GB |
| Disco SSD | 20 GB libres |
| Resolución | 1920x1080 |

---

# Sistema Operativo

Sistemas soportados:

| Sistema | Estado |
|----------|--------|
| Windows 11 | ✅ Oficial |
| Ubuntu 24.04 LTS | ✅ Oficial |
| macOS Sonoma o superior | ✅ Oficial |

---

# Versiones oficiales

| Software | Versión |
|-----------|----------|
| PHP | 8.4.x |
| Laravel | 12.x |
| Composer | 2.x |
| Node.js | 22 LTS |
| npm | 10.x o superior |
| PostgreSQL | 17.x |
| Git | Última versión estable |
| Docker Desktop | Última versión estable (opcional) |

> Las versiones podrán actualizarse mediante un ADR cuando sea necesario.

---

# Herramientas obligatorias

Todo desarrollador deberá instalar:

- Git
- PHP
- Composer
- Node.js
- npm
- PostgreSQL
- Visual Studio Code

---

# Extensiones recomendadas para VS Code

- PHP Intelephense
- Laravel Extension Pack
- Laravel Blade Formatter
- Laravel Pint
- EditorConfig
- GitLens
- Error Lens
- DotENV
- Docker
- ESLint
- Prettier
- Markdown All in One
- Markdown Preview Mermaid Support

---

# Configuración de Git

Verificar:

```bash
git --version
```

Configurar:

```bash
git config --global user.name "Tu Nombre"

git config --global user.email "correo@ejemplo.com"
```

Configurar salto de línea:

Windows

```bash
git config --global core.autocrlf true
```

Linux/macOS

```bash
git config --global core.autocrlf input
```

---

# Clonar el repositorio

```bash
git clone https://github.com/homecapital-dev/homecapital.git

cd homecapital
```

---

# Configuración del Backend

Instalar dependencias:

```bash
composer install
```

Copiar archivo de entorno:

```bash
cp .env.example .env
```

Generar la clave de la aplicación:

```bash
php artisan key:generate
```

---

# Configuración de la Base de Datos

Crear una base de datos PostgreSQL.

Ejemplo:

```
homecapital_dev
```

Actualizar el archivo `.env`:

```env
DB_CONNECTION=pgsql
DB_HOST=127.0.0.1
DB_PORT=5432
DB_DATABASE=homecapital_dev
DB_USERNAME=postgres
DB_PASSWORD=******
```

Ejecutar migraciones:

```bash
php artisan migrate
```

---

# Configuración del Frontend

Instalar dependencias:

```bash
npm install
```

Iniciar Vite:

```bash
npm run dev
```

---

# Ejecutar el proyecto

Backend:

```bash
php artisan serve
```

Frontend:

```bash
npm run dev
```

---

# Verificaciones iniciales

Antes de comenzar el desarrollo comprobar:

```bash
php artisan about

php artisan test

composer validate

composer audit

npm audit

npm run build
```

---

# Variables de entorno

Reglas:

- Nunca subir `.env`.
- Mantener `.env.example` actualizado.
- Documentar nuevas variables.
- Eliminar variables obsoletas.

---

# Estructura esperada del proyecto

```text
app/
bootstrap/
config/
database/
docs/
public/
resources/
routes/
storage/
tests/
```

---

# Flujo de trabajo diario

1. Actualizar la rama principal.

```bash
git checkout main

git pull origin main
```

2. Crear una nueva rama.

```bash
git checkout -b feature/HC-015-example
```

3. Desarrollar la funcionalidad.

4. Ejecutar validaciones.

```bash
php artisan test

npm run build
```

5. Crear commits siguiendo Conventional Commits.

6. Enviar la rama.

```bash
git push origin feature/HC-015-example
```

7. Crear Pull Request.

---

# Solución de problemas

## Error en Composer

```bash
composer diagnose
```

---

## Error de permisos

Ejecutar:

```bash
php artisan optimize:clear
```

---

## Error en Node

Eliminar:

```
node_modules/
package-lock.json
```

Luego:

```bash
npm install
```

---

## Error de caché

```bash
php artisan optimize:clear
```

---

## Error de migraciones

```bash
php artisan migrate:fresh
```

> Solo utilizar en entornos de desarrollo.

---

# Checklist

Antes de comenzar a desarrollar verificar:

- [ ] Git instalado.
- [ ] PHP instalado.
- [ ] Composer instalado.
- [ ] Node.js instalado.
- [ ] PostgreSQL instalado.
- [ ] Dependencias instaladas.
- [ ] Variables de entorno configuradas.
- [ ] Base de datos creada.
- [ ] Migraciones ejecutadas.
- [ ] Proyecto inicia correctamente.

---

# Roadmap

Sprint 1

- Configuración inicial del backend.

Sprint 2

- Docker Compose.

Sprint 3

- Dev Containers.

Sprint 4

- Automatización del entorno.

---

# Referencias

- Laravel Documentation
- Composer Documentation
- Node.js Documentation
- PostgreSQL Documentation
- Visual Studio Code Documentation

---

# Historial

| Versión | Fecha | Descripción |
|----------|-------|-------------|
| 1.0.0 | 2026-08-04 | Creación del documento |
