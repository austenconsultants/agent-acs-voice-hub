# ACS Voice Hub Agent

## Overview
Voice Hub manages FreeSWITCH integration and telephony operations.

## Components
- **Frontend**: React UI on Node.js (Port 3211)
- **Backend**: FreeSWITCH (10.152.0.77)
- **Database**: PostgreSQL + Valkey
- **Integration**: Direct connection to Voice Agent

## Architecture
```
Voice Hub (3211)
    ├── React UI
    ├── FreeSWITCH Control
    ├── SIP Management
    └── Call Routing
```

## Context Keys
- `voice_hub.config` - Current configuration
- `voice_hub.active_calls` - Live call state
- `voice_hub.sip_registrations` - SIP endpoints
- `voice_hub.ivr_flows` - IVR configurations
