# Evaluación de memoria conversacional (n8n)

## 1) Nodos `@n8n/n8n-nodes-langchain.memoryPostgresChat` detectados

### `MainBot.json`
- `Chat Memory2`
- `Chat Memory1`
- `Postgres Chat Memory`
- `Postgres Chat Memory1`

### `NewsFlows.json`
- `Chat Memory`

## 2) Decisión tomada

**Se mantiene temporalmente la memoria en Postgres** para evitar regresiones operativas inmediatas en los agentes ya desplegados.

### Justificación
- El repositorio actual solo contiene flujos n8n (`MainBot.json`, `NewsFlows.json`, `Processing Incoming Message 2.0.json`) y **no incluye código backend** para implementar aquí mismo endpoints nuevos.
- Los nodos de memoria están acoplados a agentes en producción; migrarlos sin backend versionado en este repo eleva riesgo.

## 3) Plan de migración recomendado (fase siguiente)

Cuando el backend esté disponible en este repositorio o en un servicio versionado:

1. Crear endpoint **append message**:
   - `POST /api/chat-histories/append`
   - Body sugerido:
     ```json
     {
       "session_id": "string",
       "message": {
         "type": "human|ai",
         "content": "string",
         "data": { "content": "string" }
       },
       "metadata": {}
     }
     ```

2. Crear endpoint **get conversation window**:
   - `GET /api/chat-histories/session/:session_id/window?limit=30`
   - Respuesta sugerida:
     ```json
     {
       "session_id": "string",
       "messages": [
         { "type": "human", "content": "...", "data": { "content": "..." } }
       ]
     }
     ```

3. En n8n:
   - Sustituir `memoryPostgresChat` por nodos HTTP Request al backend.
   - Inyectar historial formateado en `systemMessage` o en un campo `history_context` previo al nodo IA.

## 4) Validación del code node `Formatear Conversacion`

Se reforzó el código para validar explícitamente la estructura esperada de `message`:
- `type`
- `content`
- `data.content`

Además, ahora tolera variantes de payload (`role`, `content` en niveles alternos) y marca entradas inesperadas para diagnóstico.
