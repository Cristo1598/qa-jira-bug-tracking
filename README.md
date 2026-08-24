# QA Bug Tracking — Jira

Práctica personal de gestión del ciclo de vida de incidencias (bugs) en Jira, documentando defectos identificados durante las pruebas de API realizadas con Postman sobre **reqres.in** y **JSONPlaceholder**.

Este repositorio forma parte de mi proceso de transición profesional hacia QA/Testing, aplicando conceptos de:

- Redacción de bugs con pasos de reproducción claros
- Distinción entre resultado esperado vs. resultado obtenido
- Priorización de incidencias (triage)
- Gestión del ciclo de vida de un defecto en un tablero Kanban

> **Nota:** los bugs documentados aquí son **simulados con fines de práctica**, basados en patrones reales de defectos que suelen encontrarse en APIs REST (falta de validaciones, inconsistencia de contratos entre endpoints). No corresponden a hallazgos en un sistema en producción.

---

## 🛠️ Herramienta utilizada

**Jira Cloud** (proyecto tipo Kanban) — `solisjimenescristo.atlassian.net`

---

## 📋 Tablero general

3 issues de tipo **Error (Bug)** en la columna "Por hacer", cada uno con prioridad asignada y responsable.

---

## 🐛 Bugs documentados

### KAN-1 — Falta de validación de formato de email al crear usuario

| Campo | Detalle |
|---|---|
| **API** | reqres.in |
| **Prioridad** | Media |
| **Pasos para reproducir** | 1. Enviar `POST /api/users` <br> 2. Body: `{ "name": "Test", "job": "QA", "email": "correo-invalido" }` <br> 3. Observar la respuesta |
| **Resultado esperado** | Código 400 Bad Request, indicando formato de email inválido |
| **Resultado obtenido** | 201 Created, sin validar el formato del campo `email` |

---

### KAN-2 — Inconsistencia de código HTTP en operación DELETE entre APIs equivalentes

| Campo | Detalle |
|---|---|
| **API** | reqres.in / JSONPlaceholder |
| **Prioridad** | Baja |
| **Pasos para reproducir** | 1. Ejecutar `DELETE /api/users/2` en reqres.in <br> 2. Ejecutar `DELETE /posts/1` en JSONPlaceholder <br> 3. Comparar los códigos de respuesta HTTP |
| **Resultado esperado** | Ambas operaciones deberían seguir un contrato de respuesta consistente (por convención REST, 204 No Content sin body) |
| **Resultado obtenido** | reqres.in devuelve 204 No Content; JSONPlaceholder devuelve 200 OK con body vacío `{}` |

---

### KAN-3 — Falta de validación de campo "title" vacío al crear post

| Campo | Detalle |
|---|---|
| **API** | JSONPlaceholder |
| **Prioridad** | Media |
| **Pasos para reproducir** | 1. Enviar `POST /posts` <br> 2. Body: `{ "title": "", "body": "Contenido de prueba", "userId": 1 }` <br> 3. Observar la respuesta |
| **Resultado esperado** | Código 400 Bad Request, indicando que `title` es obligatorio |
| **Resultado obtenido** | 201 Created, sin validar que `title` tenga contenido |

---

## 📂 Contenido del repositorio

```
qa-jira-bug-tracking/
├── README.md
└── screenshots/
    ├── 01-tablero-general.png
    ├── 02-bug-KAN-1.png
    ├── 03-bug-KAN-2.png
    └── 04-bug-KAN-3.png
```

---

## 💡 Aprendizajes

- Redactar un bug de forma clara y reproducible, no solo describir el síntoma
- Diferenciar resultado esperado vs. obtenido como base de cualquier reporte de incidencia
- Priorizar defectos según su impacto real (no todos los bugs tienen la misma severidad)
- Documentar hallazgos de forma que sean verificables, incluso cuando son ejercicios de práctica
