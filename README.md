# README - Mapa actual de workflows n8n

Este documento describe el estado **actual** de los workflows exportados en este repositorio.

## MainBot (`MainBot.json`)

- Activo: `True`
- Total de nodos: `59`

### Triggers de entrada
- `WhatsApp Trigger` · `n8n-nodes-base.whatsAppTrigger`

### Llamadas a sub-workflows
- `Call 'Processing Incoming Message 2.0'` -> `Processing Incoming Message 2.0`
- `Call 'NewsFlows'` -> `NewsFlows`

### Rutas HTTP usadas por nodos
| Nodo | URL |
|---|---|
| `SET: BOT FREE` | `=https://vg.g210512.com/api/bot-users/session/{{ $("Call 'Processing Incoming Message 2.0'").item.json.session_id }}` |
| `Guardar Veto Postgress1` | `=https://vg.g210512.com/api/bot-users/session/{{ $("Call 'Processing Incoming Message 2.0'").item.json.session_id }}` |
| `API: Add Comment` | `=https://vg.g210512.com/api/v1/contactos/{{ $('Guardar Veto Postgress1').item.json.api_contact_id }}/comentarios` |
| `GET: Chat Histories1` | `=https://crm.g210512.com/api/chat-histories/session/{{ $("Call 'Processing Incoming Message 2.0'").item.json.session_id }}?order=desc&limit=10` |
| `SET: BOT FREE1` | `=https://vg.g210512.com/api/bot-users/session/{{ $("Call 'Processing Incoming Message 2.0'").item.json.session_id }}` |
| `SET: Rejected Status2` | `=https://vg.g210512.com/api/v1/contactos/{{ $('Guardar Veto Postgress1').item.json.api_contact_id }}/estado` |
| `Incrementar Contador y Bloquear` | `=https://vg.g210512.com/api/bot-users/session/{{ $("Call 'Processing Incoming Message 2.0'").item.json.session_id }}/counters` |
| `SET: Blocked Status2` | `=https://vg.g210512.com/api/v1/contactos/{{ $json.api_contact_id }}/estado` |
| `SET: Blocked1` | `=https://vg.g210512.com/api/bot-users/session/{{ $("Call 'Processing Incoming Message 2.0'").item.json.session_id }}` |
| `API: Add Comment2` | `=https://vg.g210512.com/api/v1/contactos/{{ $json.data.id }}/comentarios` |
| `SET prospecting status1` | `=https://vg.g210512.com/api/bot-users/session/{{ $("Call 'Processing Incoming Message 2.0'").item.json.session_id }}` |
| `API - Add Property Interest` | `=https://vg.g210512.com/api/v1/contactos/{{ $('Switch: Actual status').first().json.api_contact_id }}/intereses` |
| `User Reject Q` | `=https://vg.g210512.com/api/bot-users/session/{{ $("Call 'Processing Incoming Message 2.0'").item.json.session_id }}` |
| `Set Retry` | `=https://vg.g210512.com/api/bot-users/session/{{ $("Call 'Processing Incoming Message 2.0'").item.json.session_id }}` |
| `Set Status Accepted` | `=https://vg.g210512.com/api/bot-users/session/{{ $("Call 'Processing Incoming Message 2.0'").item.json.session_id }}` |
| `Get Audio` | `={{ $json.url }}` |
| `GET: Chat Histories (Wide Context)` | `=https://crm.g210512.com/api/chat-histories/session/{{ $("Call 'Processing Incoming Message 2.0'").item.json.session_id }}?order=asc&limit=200&page=1` |

### Inventario de nodos
| Nodo | Tipo |
|---|---|
| `Switch: Actual status` | `n8n-nodes-base.switch` |
| `consultar_inmuebles1` | `@n8n/n8n-nodes-langchain.vectorStorePGVector` |
| `No Operation, do nothing` | `n8n-nodes-base.noOp` |
| `AI: Buscador` | `@n8n/n8n-nodes-langchain.agent` |
| `Switch` | `n8n-nodes-base.switch` |
| `AI Cleaner - Buscador` | `n8n-nodes-base.code` |
| `SET: BOT FREE` | `n8n-nodes-base.httpRequest` |
| `Guardar Veto Postgress1` | `n8n-nodes-base.httpRequest` |
| `API: Add Comment` | `n8n-nodes-base.httpRequest` |
| `GET: Chat Histories1` | `n8n-nodes-base.httpRequestTool` |
| `SET: BOT FREE1` | `n8n-nodes-base.httpRequest` |
| `SET: Rejected Status2` | `n8n-nodes-base.httpRequest` |
| `Incrementar Contador y Bloquear` | `n8n-nodes-base.httpRequest` |
| `If: Block Limit Reached?` | `n8n-nodes-base.if` |
| `SET: Blocked Status2` | `n8n-nodes-base.httpRequest` |
| `SET: Blocked1` | `n8n-nodes-base.httpRequest` |
| `API: Add Comment2` | `n8n-nodes-base.httpRequest` |
| `Message a model2` | `@n8n/n8n-nodes-langchain.openAi` |
| `Reject Chat2` | `n8n-nodes-base.telegram` |
| `Sticky Note2` | `n8n-nodes-base.stickyNote` |
| `Send a text message1` | `n8n-nodes-base.telegram` |
| `OpenAI Chat Model1` | `@n8n/n8n-nodes-langchain.lmChatOpenAi` |
| `SET prospecting status1` | `n8n-nodes-base.httpRequest` |
| `API - Add Property Interest` | `n8n-nodes-base.httpRequest` |
| `AI: Generate Reject Message1` | `@n8n/n8n-nodes-langchain.openAi` |
| `Sticky Note4` | `n8n-nodes-base.stickyNote` |
| `If: Agree?` | `n8n-nodes-base.if` |
| `AI: Agree w Questionaire?` | `@n8n/n8n-nodes-langchain.openAi` |
| `Parse Response Boolean` | `n8n-nodes-base.code` |
| `Switch: Questionnaire Status` | `n8n-nodes-base.switch` |
| `Set: Despedida` | `n8n-nodes-base.set` |
| `User Reject Q` | `n8n-nodes-base.httpRequest` |
| `Response: User Rejects Q` | `n8n-nodes-base.telegram` |
| `Response: User change mind?` | `n8n-nodes-base.telegram` |
| `Set Retry` | `n8n-nodes-base.httpRequest` |
| `Set Status Accepted` | `n8n-nodes-base.httpRequest` |
| `Chat Memory2` | `@n8n/n8n-nodes-langchain.memoryPostgresChat` |
| `consultar_inmuebles` | `@n8n/n8n-nodes-langchain.vectorStorePGVector` |
| `OpenAI Chat Model2` | `@n8n/n8n-nodes-langchain.lmChatOpenAi` |
| `AI: Questionaire` | `@n8n/n8n-nodes-langchain.agent` |
| `Embeddings Google Gemini` | `@n8n/n8n-nodes-langchain.embeddingsGoogleGemini` |
| `AI Agent` | `@n8n/n8n-nodes-langchain.agent` |
| `OpenAI Chat Model3` | `@n8n/n8n-nodes-langchain.lmChatOpenAi` |
| `AI Cleaner` | `n8n-nodes-base.code` |
| `Switch1` | `n8n-nodes-base.switch` |
| `AI Agent1` | `@n8n/n8n-nodes-langchain.agent` |
| `Chat Memory1` | `@n8n/n8n-nodes-langchain.memoryPostgresChat` |
| `Postgres Chat Memory` | `@n8n/n8n-nodes-langchain.memoryPostgresChat` |
| `OpenAI Chat Model4` | `@n8n/n8n-nodes-langchain.lmChatOpenAi` |
| `Postgres Chat Memory1` | `@n8n/n8n-nodes-langchain.memoryPostgresChat` |
| `WhatsApp Trigger` | `n8n-nodes-base.whatsAppTrigger` |
| `Get Audio` | `n8n-nodes-base.httpRequest` |
| `Transcribe a recording` | `@n8n/n8n-nodes-langchain.openAi` |
| `Switch Type Of Message` | `n8n-nodes-base.switch` |
| `Call 'Processing Incoming Message 2.0'` | `n8n-nodes-base.executeWorkflow` |
| `Call 'NewsFlows'` | `n8n-nodes-base.executeWorkflow` |
| `Política Historial Chat` | `n8n-nodes-base.stickyNote` |
| `GET: Chat Histories (Wide Context)` | `n8n-nodes-base.httpRequestTool` |
| `Code: Concat Chat Pages` | `n8n-nodes-base.code` |

### Mapa de conexiones
| Origen | Tipo de conexión | Destino |
|---|---|---|
| `Switch: Actual status` | `main[0]` | `Switch: Questionnaire Status` |
| `Switch: Actual status` | `main[1]` | `Call 'NewsFlows'` |
| `Switch: Actual status` | `main[2]` | `Incrementar Contador y Bloquear` |
| `Switch: Actual status` | `main[3]` | `No Operation, do nothing` |
| `consultar_inmuebles1` | `ai_tool[0]` | `AI: Buscador` |
| `AI: Buscador` | `main[0]` | `AI Cleaner - Buscador` |
| `Switch` | `main[0]` | `API - Add Property Interest` |
| `Switch` | `main[1]` | `∅` |
| `Switch` | `main[2]` | `Guardar Veto Postgress1` |
| `Switch` | `main[3]` | `∅` |
| `AI Cleaner - Buscador` | `main[0]` | `Switch` |
| `Guardar Veto Postgress1` | `main[0]` | `∅` |
| `API: Add Comment` | `main[0]` | `SET: Rejected Status2` |
| `GET: Chat Histories1` | `ai_tool[0]` | `AI: Generate Reject Message1` |
| `SET: Rejected Status2` | `main[0]` | `SET: BOT FREE1` |
| `Incrementar Contador y Bloquear` | `main[0]` | `If: Block Limit Reached?` |
| `If: Block Limit Reached?` | `main[0]` | `SET: Blocked1` |
| `If: Block Limit Reached?` | `main[1]` | `Message a model2` |
| `SET: Blocked1` | `main[0]` | `SET: Blocked Status2` |
| `SET: Blocked Status2` | `main[0]` | `API: Add Comment2` |
| `API: Add Comment2` | `main[0]` | `Send a text message1` |
| `Message a model2` | `main[0]` | `Reject Chat2` |
| `Reject Chat2` | `main[0]` | `SET: BOT FREE` |
| `Send a text message1` | `main[0]` | `SET: BOT FREE` |
| `OpenAI Chat Model1` | `ai_languageModel[0]` | `AI: Buscador` |
| `SET prospecting status1` | `main[0]` | `SET: BOT FREE1` |
| `API - Add Property Interest` | `main[0]` | `∅` |
| `AI: Generate Reject Message1` | `main[0]` | `API: Add Comment` |
| `AI: Agree w Questionaire?` | `main[0]` | `Parse Response Boolean` |
| `Parse Response Boolean` | `main[0]` | `If: Agree?` |
| `Switch: Questionnaire Status` | `main[0]` | `Response: User change mind?` |
| `Switch: Questionnaire Status` | `main[1]` | `∅` |
| `Switch: Questionnaire Status` | `main[2]` | `∅` |
| `Switch: Questionnaire Status` | `main[3]` | `AI: Agree w Questionaire?` |
| `Switch: Questionnaire Status` | `main[4]` | `AI: Agree w Questionaire?` |
| `If: Agree?` | `main[0]` | `Set Status Accepted` |
| `If: Agree?` | `main[1]` | `Set: Despedida` |
| `Set: Despedida` | `main[0]` | `User Reject Q` |
| `User Reject Q` | `main[0]` | `Response: User Rejects Q` |
| `Response: User change mind?` | `main[0]` | `Set Retry` |
| `Chat Memory2` | `ai_memory[0]` | `AI: Questionaire` |
| `consultar_inmuebles` | `ai_tool[0]` | `AI: Questionaire` |
| `OpenAI Chat Model2` | `ai_languageModel[0]` | `AI: Questionaire` |
| `Set Status Accepted` | `main[0]` | `AI: Questionaire` |
| `Embeddings Google Gemini` | `ai_embedding[0]` | `consultar_inmuebles1` |
| `AI Agent` | `main[0]` | `∅` |
| `OpenAI Chat Model3` | `ai_languageModel[0]` | `AI Agent` |
| `AI Cleaner` | `main[0]` | `Switch1` |
| `Switch1` | `main[0]` | `AI Agent1` |
| `Switch1` | `main[1]` | `∅` |
| `Switch1` | `main[2]` | `∅` |
| `Switch1` | `main[3]` | `∅` |
| `Chat Memory1` | `ai_memory[0]` | `AI: Buscador` |
| `Postgres Chat Memory` | `ai_memory[0]` | `AI Agent` |
| `OpenAI Chat Model4` | `ai_languageModel[0]` | `AI Agent1` |
| `Postgres Chat Memory1` | `ai_memory[0]` | `AI Agent1` |
| `WhatsApp Trigger` | `main[0]` | `Switch Type Of Message` |
| `Get Audio` | `main[0]` | `Transcribe a recording` |
| `Transcribe a recording` | `main[0]` | `∅` |
| `Switch Type Of Message` | `main[0]` | `Call 'Processing Incoming Message 2.0'` |
| `Switch Type Of Message` | `main[1]` | `∅` |
| `Switch Type Of Message` | `main[2]` | `∅` |
| `Switch Type Of Message` | `main[3]` | `∅` |
| `Switch Type Of Message` | `main[4]` | `∅` |
| `Switch Type Of Message` | `main[5]` | `∅` |
| `Call 'Processing Incoming Message 2.0'` | `main[0]` | `Switch: Actual status` |

## Processing Incoming Message 2.0 (`Processing Incoming Message 2.0.json`)

- Activo: `True`
- Total de nodos: `14`

### Triggers de entrada
- `When Executed by Another Workflow` · `n8n-nodes-base.executeWorkflowTrigger`

### Rutas HTTP usadas por nodos
| Nodo | URL |
|---|---|
| `GET: Contact Info` | `=https://vg.g210512.com/api/bot-users/session/{{ $json.wa_id }}` |
| `Get API Contact` | `=https://vg.g210512.com/api/v1/contactos?telefono={{ $('When Executed by Another Workflow').item.json.wa_id.slice(3) }}` |
| `Create API Contact` | `https://vg.g210512.com/api/v1/contactos` |
| `Create Postgress Contact` | `=https://vg.g210512.com/api/bot-users/upsert` |
| `Insert After API Creation` | `=https://vg.g210512.com/api/bot-users/upsert` |
| `SET: Bot processing` | `=https://vg.g210512.com/api/bot-users/session/{{ $('When Executed by Another Workflow').item.json.wa_id }}` |

### Inventario de nodos
| Nodo | Tipo |
|---|---|
| `When Executed by Another Workflow` | `n8n-nodes-base.executeWorkflowTrigger` |
| `GET: Contact Info` | `n8n-nodes-base.httpRequest` |
| `Get API Contact` | `n8n-nodes-base.httpRequest` |
| `Create API Contact` | `n8n-nodes-base.httpRequest` |
| `If exists in Postgress?` | `n8n-nodes-base.if` |
| `If: Exist in API?` | `n8n-nodes-base.if` |
| `Create Postgress Contact` | `n8n-nodes-base.httpRequest` |
| `Insert After API Creation` | `n8n-nodes-base.httpRequest` |
| `SET: Bot processing` | `n8n-nodes-base.httpRequest` |
| `If: Bot is processing` | `n8n-nodes-base.if` |
| `Set: Contact Data Info` | `n8n-nodes-base.set` |
| `Send message` | `n8n-nodes-base.whatsApp` |
| `Set: Contact Data Info1` | `n8n-nodes-base.set` |
| `Set: Contact Data Info2` | `n8n-nodes-base.set` |

### Mapa de conexiones
| Origen | Tipo de conexión | Destino |
|---|---|---|
| `GET: Contact Info` | `main[0]` | `If: Bot is processing` |
| `Get API Contact` | `main[0]` | `If: Exist in API?` |
| `Create API Contact` | `main[0]` | `Insert After API Creation` |
| `If exists in Postgress?` | `main[0]` | `Set: Contact Data Info1` |
| `If exists in Postgress?` | `main[1]` | `Get API Contact` |
| `If: Exist in API?` | `main[0]` | `Create Postgress Contact` |
| `If: Exist in API?` | `main[1]` | `Create API Contact` |
| `Create Postgress Contact` | `main[0]` | `Set: Contact Data Info2` |
| `Insert After API Creation` | `main[0]` | `Set: Contact Data Info` |
| `SET: Bot processing` | `main[0]` | `If exists in Postgress?` |
| `If: Bot is processing` | `main[0]` | `Send message` |
| `If: Bot is processing` | `main[1]` | `SET: Bot processing` |
| `When Executed by Another Workflow` | `main[0]` | `GET: Contact Info` |

## NewsFlows (`NewsFlows.json`)

- Activo: `True`
- Total de nodos: `26`

### Triggers de entrada
- `When Executed by Another Workflow` · `n8n-nodes-base.executeWorkflowTrigger`

### Rutas HTTP usadas por nodos
| Nodo | URL |
|---|---|
| `Guardar Veto Postgress` | `=https://vg.g210512.com/api/bot-users/session/{{ $('When Executed by Another Workflow').first().json.session_id }}` |
| `HTTP Request1` | `=https://vg.g210512.com/api/v1/contactos/{{ $('SET: Blocked Status').first().json.data.id }}/comentarios` |
| `Get Story Chat` | `=https://crm.g210512.com/api/chat-histories/session/{{ $json.session_id }}?order=desc&limit=10` |
| `SET: Blocked` | `=https://vg.g210512.com/api/bot-users/session/{{ $('When Executed by Another Workflow').item.json.session_id }}` |
| `SET prospecting status` | `=https://vg.g210512.com/api/bot-users/session/{{ $('When Executed by Another Workflow').first().json.session_id }}` |
| `API: Add Comment1` | `=https://vg.g210512.com/api/v1/contactos/{{ $('AI Cleaner - Recepcionista').item.json.api_id }}/comentarios` |
| `GET: Chat Histories` | `=https://crm.g210512.com/api/chat-histories/session/{{ $('When Executed by Another Workflow').first().json.session_id }}?order=desc&limit=10` |
| `SET: Blocked Status` | `=https://vg.g210512.com/api/v1/contactos/{{ $json.api_contact_id }}/estado` |
| `SET: Blocked Status1` | `=https://vg.g210512.com/api/v1/contactos/{{ $('AI Cleaner - Recepcionista').item.json.api_id }}/estado` |
| `API: Update Contact` | `=https://vg.g210512.com/api/v1/contactos/{{ $('AI Cleaner - Recepcionista').item.json.api_id }}` |
| `SET: Prospecting Status` | `=https://vg.g210512.com/api/v1/contactos/{{ $('AI Cleaner - Recepcionista').item.json.api_id }}/estado` |
| `SET: BOT FREE2` | `=https://vg.g210512.com/api/bot-users/session/{{ $('Query de Actualización Inteligente').item.json.session_id }}` |

### Inventario de nodos
| Nodo | Tipo |
|---|---|
| `Guardar Veto Postgress` | `n8n-nodes-base.httpRequest` |
| `HTTP Request1` | `n8n-nodes-base.httpRequest` |
| `Formatear Conversacion` | `n8n-nodes-base.code` |
| `Get Story Chat` | `n8n-nodes-base.httpRequest` |
| `SET: Blocked` | `n8n-nodes-base.httpRequest` |
| `Switch: Block or Continue` | `n8n-nodes-base.switch` |
| `Chat Memory` | `@n8n/n8n-nodes-langchain.memoryPostgresChat` |
| `AI: Recepcionista` | `@n8n/n8n-nodes-langchain.agent` |
| `SET prospecting status` | `n8n-nodes-base.httpRequest` |
| `Reject Chat` | `n8n-nodes-base.telegram` |
| `Transfer Chat` | `n8n-nodes-base.telegram` |
| `OpenAI Chat Model` | `@n8n/n8n-nodes-langchain.lmChatOpenAi` |
| `API: Add Comment1` | `n8n-nodes-base.httpRequest` |
| `GET: Chat Histories` | `n8n-nodes-base.httpRequestTool` |
| `SET: Blocked Status` | `n8n-nodes-base.httpRequest` |
| `SET: Blocked Status1` | `n8n-nodes-base.httpRequest` |
| `API: Update Contact` | `n8n-nodes-base.httpRequest` |
| `SET: Prospecting Status` | `n8n-nodes-base.httpRequest` |
| `AI Cleaner - Recepcionista` | `n8n-nodes-base.code` |
| `AI: Generate Reject Message` | `@n8n/n8n-nodes-langchain.openAi` |
| `SET: BOT FREE2` | `n8n-nodes-base.httpRequest` |
| `When Executed by Another Workflow` | `n8n-nodes-base.executeWorkflowTrigger` |
| `Send message` | `n8n-nodes-base.whatsApp` |
| `Switch` | `n8n-nodes-base.switch` |
| `Send message1` | `n8n-nodes-base.whatsApp` |
| `Set: Chat Histories Shape` | `n8n-nodes-base.set` |

### Mapa de conexiones
| Origen | Tipo de conexión | Destino |
|---|---|---|
| `Guardar Veto Postgress` | `main[0]` | `Reject Chat` |
| `Formatear Conversacion` | `main[0]` | `HTTP Request1` |
| `Get Story Chat` | `main[0]` | `Set: Chat Histories Shape` |
| `SET: Blocked` | `main[0]` | `SET: Blocked Status` |
| `Switch: Block or Continue` | `main[0]` | `Send message1` |
| `Switch: Block or Continue` | `main[1]` | `Switch` |
| `Switch: Block or Continue` | `main[2]` | `Guardar Veto Postgress` |
| `Switch: Block or Continue` | `main[3]` | `SET prospecting status` |
| `Chat Memory` | `ai_memory[0]` | `AI: Recepcionista` |
| `AI: Recepcionista` | `main[0]` | `AI Cleaner - Recepcionista` |
| `SET prospecting status` | `main[0]` | `Transfer Chat` |
| `Reject Chat` | `main[0]` | `AI: Generate Reject Message` |
| `Transfer Chat` | `main[0]` | `SET: Prospecting Status` |
| `OpenAI Chat Model` | `ai_languageModel[0]` | `AI: Recepcionista` |
| `API: Add Comment1` | `main[0]` | `SET: Blocked Status1` |
| `GET: Chat Histories` | `ai_tool[0]` | `AI: Generate Reject Message` |
| `SET: Blocked Status` | `main[0]` | `Get Story Chat` |
| `API: Update Contact` | `main[0]` | `SET: BOT FREE2` |
| `AI Cleaner - Recepcionista` | `main[0]` | `Switch: Block or Continue` |
| `AI: Generate Reject Message` | `main[0]` | `API: Add Comment1` |
| `When Executed by Another Workflow` | `main[0]` | `AI: Recepcionista` |
| `Send message` | `main[0]` | `API: Update Contact` |
| `Send message1` | `main[0]` | `SET: Blocked` |
| `Switch` | `main[0]` | `Send message` |
| `Switch` | `main[1]` | `Send message` |
| `Switch` | `main[2]` | `Send message` |
| `Set: Chat Histories Shape` | `main[0]` | `Formatear Conversacion` |

## Notas
- Este README es un inventario técnico de los exports actuales.
- Puede incluir nodos legacy o ramas vacías (`∅`) que no necesariamente se ejecutan en producción.
