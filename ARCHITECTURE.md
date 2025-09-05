# 📞 ACS-Voice Architecture

## Component Overview

```
                    ┌────────────────────┐
                    │     ACS-Voice      │
                    │  Voice Platform    │
                    └─────────┬──────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
   ┌────▼─────┐         ┌────▼─────┐         ┌────▼─────┐
   │FreeSWITCH│         │  ACS UI  │         │   IVR    │
   │  Server  │         │ Frontend │         │ Designer │
   └────┬─────┘         └────┬─────┘         └────┬─────┘
        │                     │                     │
        └─────────────────────┼─────────────────────┘
                              │
                    ┌─────────▼──────────┐
                    │  Integration Layer  │
                    │                     │
                    │ • Receives AI specs │
                    │ • Updates routing   │
                    │ • Manages calls     │
                    └─────────────────────┘
```

## Connection Points

### Incoming Connections
- **From ACS-Manager**: Platform configuration requests
- **From ACS-Voice-Agent**: AI configuration specs
- **From Twilio**: SIP trunk connections
- **From Users**: Web UI access (port 3211)

### Outgoing Connections
- **To FreeSWITCH**: ESL commands (10.152.0.77:8021)
- **To Database**: Configuration storage
- **To ACS-Voice-Agent**: AI enhancement requests

## FreeSWITCH Integration

```xml
<!-- Dialplan Example -->
<extension name="acs_ivr">
  <condition field="destination_number" expression="^1000$">
    <action application="answer"/>
    <action application="playback" data="welcome.wav"/>
    <action application="ivr" data="main_menu"/>
  </condition>
</extension>
```

## Database Schema

```sql
-- FreeSWITCH Configuration
freeswitch_knowledge (
    template_name, xml_config,
    description, category
)

-- IVR Flows
ivr_templates (
    flow_id, menu_structure,
    prompts, actions
)

-- SIP Trunks
sip_trunk_configs (
    provider, credentials,
    settings, active
)
```

## UI Access Points

- **Main UI**: http://10.152.0.71:3211
- **API**: http://10.152.0.71:3211/api
- **WebSocket**: ws://10.152.0.71:3211/ws

---
*Part of AustenTel ACS Platform*
