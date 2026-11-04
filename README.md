# Checkpoint 4 · Integraciones avanzadas (HubSpot + Gmail + Slack)

**Alumno:** Franco Scigliano · **Curso:** AI Automation Avanzado (Coderhouse)

## Qué hace el workflow
Cuando llega un correo de un cliente a soporte (asunto con `SOPORTE`), el flujo:

1. **Gmail Trigger** detecta el correo nuevo (revisa cada minuto).
2. **IF · ¿Es auto-reply?** descarta respuestas automáticas, `no-reply` y `mailer-daemon` (evita bucles infinitos).
3. **Set · Limpiar payload** deja solo email, nombre, asunto, cuerpo (máx. 2000 caracteres) y threadId.
4. **IF · ¿Email válido?** corta si el email no tiene formato válido (evita el error 400 de HubSpot).
5. **IA · Redactar borrador** (gpt-4o-mini) escribe una respuesta cordial sin inventar precios, stock ni fechas.
6. **HubSpot · Look up** busca el contacto por email. **IF · ¿Existe?**: si no existe, **HubSpot · Crear contacto** (evita duplicados / error 409).
7. **Gmail · Create Draft** deja la respuesta como **borrador** (aprobación humana, no se envía sola).
8. **Slack · Avisar al equipo** publica en `#operaciones` que hay un borrador listo para aprobar.

## Buenas prácticas aplicadas
- Human-in-the-loop: la IA nunca envía, solo crea borrador.
- Anti auto-reply para cortar bucles.
- Lookup antes de crear (sin duplicados en el CRM).
- Limpieza de payload antes de cada integración.
- Mínimo privilegio: el acceso a HubSpot solo tiene permisos de lectura/escritura de contactos.

## Credenciales conectadas
![Credentials en n8n](img/credenciales.png)

Conexiones activas: **HubSpot (CRM)**, **Gmail** y **Slack**.

## Cómo importarlo
1. En n8n: **Workflows > Import from file**.
2. Elegir `checkpoint4_franco_scigliano.json`.
3. Reasignar las credenciales propias de HubSpot, Gmail, Slack y OpenAI.

## Archivos
- `checkpoint4_franco_scigliano.json`: workflow exportado de n8n.
- `img/credenciales.png`: captura de la sección Credentials.
