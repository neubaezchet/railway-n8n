# 🔐 CONFIGURACIÓN N8N - Credencial WAHA

## ✅ CONFIGURACIÓN REALIZADA

El workflow JSON ha sido actualizado con:
- ✅ Headers de autenticación: `X-API-Key: 1085043374`
- ✅ URL correcta: `https://devlikeaprowaha-production-111a.up.railway.app/api/sendText`
- ✅ chatId formateado correctamente
- ✅ Método POST con Body JSON

## 📝 SI NECESITAS HACERLO MANUALMENTE EN N8N

### Opción 1: Usar la credencial existente (Más rápido)

1. Abre N8N Dashboard
2. Ve a **Credentials** (lado izquierdo, abajo)
3. Busca **"Header Auth account"** o la que veas
4. Edítala y agrega estos headers:
   ```
   Header Name: X-API-Key
   Header Value: 1085043374
   ```
5. Guardar
6. El nodo "WAHA - Enviar WhatsApp" debería usar esa credencial

### Opción 2: Crear nueva credencial (Más seguro)

1. N8N Dashboard → **Credentials** → **+ New**
2. Tipo: **HTTP Header Auth**
3. Nombre: `WAHA API Key`
4. Headers:
   ```
   Header Name: X-API-Key
   Header Value: 1085043374
   ```
5. Click **Save & Close**
6. En el nodo WAHA, seleccionar esta credencial

### Opción 3: Variable de Entorno (Más seguro para producción)

En Railway WAHA settings:
```
WAHA_API_KEY=1085043374
```

En N8N, usar variable:
```
{{ env.WAHA_API_KEY }}
```

## 🧪 VERIFICAR QUE FUNCIONA

1. Abre el workflow "IncaNeurobaeza - Email + WhatsApp v5"
2. Haz click en **Test**
3. Usa este payload:

```json
{
  "tipo_notificacion": "confirmacion",
  "email": "test@gmail.com",
  "serial": "TEST-001",
  "subject": "Test WhatsApp con WAHA",
  "html_content": "<p>Este es un test</p>",
  "cc_email": "",
  "correo_bd": "",
  "whatsapp": "573005551234",
  "whatsapp_message": "Mensaje de prueba",
  "adjuntos": []
}
```

4. Click en **Send**
5. Ver resultado en **Executions**

## ✅ CHECKLIST

- [x] Archivo JSON actualizado con headers WAHA
- [x] API Key: 1085043374 configurada
- [ ] Hacer deploy a Railway
- [ ] Prueba en N8N Dashboard
- [ ] Enviar mensaje real para verificar

## 🚀 DEPLOY

Una vez verificado en N8N:

```bash
cd c:\Users\Administrador\Documents\GitHub
git add .
git commit -m "fix: Agregar autenticación API Key WAHA a N8N"
git push origin main
```

Railway deployará automáticamente.

## 📊 FLUJO CORRECTO AHORA

```
Backend → N8N Webhook
    ↓
N8N: Procesar Datos
    ↓ (formatea número)
N8N: ¿Enviar WhatsApp?
    ↓ (si número válido)
N8N: Split Numbers
    ↓ (divide array)
N8N: WAHA - Enviar WhatsApp
    ├─ POST /api/sendText
    ├─ Header: X-API-Key: 1085043374 ✅ AHORA INCLUIDO
    ├─ Body: { session, chatId, text }
    └─ Timeout: 30s
    ↓
WAHA (Railway)
    ├─ Autentica ✅
    ├─ Envía WhatsApp
    └─ Retorna 200 OK
    ↓
N8N: Preparar Respuesta
    └─ { channels: { email: {...}, whatsapp: {...} } }
    ↓
Backend recibe
    └─ Logea: "✅ WHATSAPP enviado"
    ↓
Frontend recibe respuesta exitosa
    └─ Muestra: "Solicitud enviada con éxito"
```

## 🔒 SEGURIDAD

**⚠️ IMPORTANTE:**
- API Key está ahora en el JSON (que va a Railway)
- En producción, usar variables de entorno
- No commitear API Keys en código

**Mejor práctica:**
```bash
# En Railway → Environment Variables:
WAHA_API_KEY=1085043374

# En N8N JSON:
"X-API-Key": "{{ env.WAHA_API_KEY }}"
```

---

**Próximo paso:** Deploy a Railway

