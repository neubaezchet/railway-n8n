# n8n IncaNeurobaeza 2025

Sistema de notificaciones automáticas para incapacidades.

## Despliegue en Railway

Este proyecto se despliega automáticamente en Railway desde el repositorio.

### Variables de entorno

Configuradas en Railway Dashboard (Variables de entorno)

### Versión

- n8n: 1.122.0
- Node: Latest LTS

### Webhooks

- Incapacidades: `https://n8n-incaneurobaeza-2025.up.railway.app/webhook/incapacidades`

### Acceso

- URL: https://n8n-incaneurobaeza-2025.up.railway.app
- Usuario: admin
- Password: 1085043374@Aa

### Notas de Despliegue

- Configuración: `railway.toml`
- Volumen persistente: `/home/node/.n8n` (1GB)
- Región: Oregon
- Health check: `/healthz`