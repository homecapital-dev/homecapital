---
Document ID: ENG-011
Title: Security Guidelines
Version: 1.0.0
Status: Draft
Owner: HomeCapital Team
Author: Andres Fonseca
Reviewer: Software Architect
Created: 2026-08-04
Last Updated: 2026-08-04
Related Sprint: Sprint 0.5
Related Issue: HC-011
Category: Engineering
---

# Guía de Seguridad

> Este documento establece las políticas y lineamientos de seguridad que deberán seguirse durante el desarrollo de HomeCapital. Su objetivo es reducir riesgos de seguridad desde la etapa de diseño hasta la operación del sistema.

---

# Objetivos

La estrategia de seguridad busca:

- Proteger la información financiera de los usuarios.
- Evitar vulnerabilidades comunes.
- Reducir la superficie de ataque.
- Facilitar auditorías.
- Cumplir con buenas prácticas internacionales.
- Incorporar la seguridad desde el diseño (Security by Design).

---

# Principios

Toda funcionalidad deberá cumplir:

- Seguridad por defecto.
- Principio del menor privilegio.
- Defensa en profundidad.
- Validación de todas las entradas.
- No confiar nunca en el cliente.
- Fallar de forma segura.
- Trazabilidad de eventos críticos.

---

# Seguridad por capas

```text
Cliente
   │
Frontend (Vue)
   │
API (Laravel)
   │
Servicios
   │
Dominio
   │
Repositorio
   │
Base de Datos
```

Cada capa deberá validar la información que recibe.

---

# Gestión de autenticación

La autenticación deberá cumplir:

- Contraseñas hasheadas con Argon2id (configuración por defecto de Laravel).
- Nunca almacenar contraseñas en texto plano.
- Tokens con expiración.
- Revocación de sesiones.
- Protección frente a fuerza bruta.
- Autenticación multifactor (roadmap).

---

# Gestión de autorización

El sistema utilizará RBAC (Role-Based Access Control).

Ejemplo:

Administrador

- Crear usuarios
- Eliminar usuarios
- Configurar sistema

Usuario

- Administrar sus cuentas
- Registrar movimientos
- Consultar reportes

Nunca validar permisos únicamente desde el frontend.

---

# Validación de entradas

Toda entrada deberá validarse.

Ejemplos:

- Form Requests.
- DTOs.
- Value Objects.
- Reglas de negocio.

Nunca confiar en:

- Formularios HTML.
- JavaScript.
- Aplicaciones móviles.

---

# Protección contra OWASP Top 10

## Broken Access Control

Medidas:

- Policies.
- Gates.
- Middleware.
- Validación de propietario del recurso.

---

## Criptographic Failures

- HTTPS obligatorio.
- Contraseñas hasheadas.
- Variables sensibles en `.env`.
- Nunca almacenar secretos en Git.

---

## Injection

Prevención:

- Eloquent ORM.
- Query Builder.
- Parámetros enlazados.
- Nunca concatenar SQL.

Correcto:

```php
User::where('email', $email)->first();
```

Incorrecto:

```php
DB::select("SELECT * FROM users WHERE email='$email'");
```

---

## Insecure Design

Todo módulo deberá:

- Tener casos de uso definidos.
- Validaciones.
- Reglas de negocio.
- Manejo de errores.

---

## Security Misconfiguration

Antes de producción verificar:

- APP_DEBUG=false
- HTTPS habilitado
- Variables de entorno configuradas
- Logs protegidos
- Directorios públicos revisados

---

## Vulnerable Components

Actualizar periódicamente:

- Laravel
- PHP
- Node
- Dependencias Composer
- Dependencias NPM

Utilizar:

```bash
composer audit

npm audit
```

---

## Authentication Failures

Evitar:

- Contraseñas débiles.
- Tokens permanentes.
- Cookies inseguras.

---

## Data Integrity Failures

Validar:

- Firmas.
- Integridad.
- Hashes.
- Eventos críticos.

---

## Logging Failures

Registrar:

- Login.
- Logout.
- Cambios de contraseña.
- Eliminaciones.
- Cambios de permisos.
- Errores críticos.

Nunca registrar:

- Contraseñas.
- Tokens.
- Datos bancarios completos.
- Información sensible.

---

# Gestión de secretos

Nunca subir al repositorio:

- `.env`
- Credenciales
- Certificados
- Llaves privadas
- Tokens
- API Keys

Todos los secretos deberán almacenarse mediante variables de entorno.

---

# Seguridad en Git

Antes de cada Push verificar:

- No existen credenciales.
- No existen archivos temporales.
- No existen dumps de base de datos.
- No existen archivos `.env`.

---

# Seguridad en Base de Datos

Toda tabla deberá:

- Tener claves primarias.
- Restricciones.
- Claves foráneas.
- Índices adecuados.

No almacenar:

- Contraseñas sin hash.
- Tokens en texto plano.
- Datos innecesarios.

---

# Seguridad de la API

Toda API deberá:

- Validar autenticación.
- Validar autorización.
- Limitar peticiones (Rate Limiting).
- Devolver errores estandarizados.
- Utilizar HTTPS.

---

# Protección CSRF

Aplicable para aplicaciones web con sesión.

Laravel deberá utilizar:

- CSRF Tokens.
- Cookies seguras.
- SameSite.

---

# Protección XSS

Siempre:

- Escapar contenido.
- Sanitizar entradas cuando aplique.
- Evitar `v-html` en Vue salvo casos controlados.

---

# Protección SQL Injection

Utilizar únicamente:

- Eloquent.
- Query Builder.
- Parámetros preparados.

Nunca concatenar consultas SQL.

---

# Protección contra fuerza bruta

Aplicar:

- Rate Limiting.
- Bloqueo temporal.
- Registro de intentos.

---

# Manejo de archivos

Antes de aceptar un archivo:

- Validar tipo.
- Validar tamaño.
- Validar extensión.
- Validar MIME Type.
- Renombrar archivo.
- Nunca ejecutar archivos subidos.

---

# Dependencias

Antes de cada Release ejecutar:

```bash
composer audit

npm audit
```

Corregir vulnerabilidades críticas antes de publicar.

---

# Checklist de Seguridad

Antes de aprobar una funcionalidad:

- [ ] Validación implementada.
- [ ] Autorización implementada.
- [ ] No existen secretos en el código.
- [ ] No existe SQL concatenado.
- [ ] Logging adecuado.
- [ ] Manejo correcto de errores.
- [ ] Dependencias verificadas.
- [ ] Rate Limiting aplicado cuando corresponda.

---

# Aplicación práctica en HomeCapital

## Crear una cuenta bancaria

Verificar:

- Usuario autenticado.
- Usuario autorizado.
- Validación del nombre.
- Evitar duplicados.
- Registrar auditoría.

---

## Registrar un gasto

Validar:

- El usuario es propietario de la cuenta.
- El presupuesto existe.
- El monto es válido.
- El saldo es suficiente.
- Registrar evento de auditoría.

---

## Exportar información

Verificar:

- Permisos.
- Filtros.
- Registro de la exportación.
- Protección de datos sensibles.

---

# Referencias

- OWASP Top 10
- OWASP ASVS
- Laravel Security Documentation
- PSR-12
- RFC 9110
- NIST Secure Software Development Framework (SSDF)

---

# Historial

| Versión | Fecha | Descripción |
|----------|-------|-------------|
| 1.0.0 | 2026-08-04 | Creación del documento |
