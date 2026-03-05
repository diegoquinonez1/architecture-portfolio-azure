# Claims Enterprise (Azure)

## Objetivo general
Diseñar e implementar una plataforma de **gestión de reclamos (claims)** para seguros, orientada a **integración enterprise** en Azure, priorizando:
- procesamiento **asíncrono confiable**,
- **trazabilidad y operación** (DLQ + runbooks + alertas),
- y controles de **seguridad** a nivel de plataforma.

Repositorio: https://github.com/diegoquinonez1/claims-enterprise-azure

---

## Caso de negocio (seguro)
Un cliente reporta un reclamo (accidente, salud, hogar). La organización debe:
- recibir la solicitud y validar datos,
- procesarla de forma asíncrona (sin bloquear al usuario),
- actualizar el estado del reclamo,
- y mantener auditoría/observabilidad para soporte y compliance.

---

## Arquitectura (mini-diagrama)

![mini-diagrama.](claims-enterprise-azure.png)
```plantuml
@startuml
title Claims Enterprise (Azure) - Mini Architecture

actor "Usuario/Canal" as U

component "Azure API Management\n(APIM)" as APIM
component "Claims.Api\n(App Service)" as API
queue "Service Bus Queue\nclaims.commands" as SBQ
database "Azure SQL\nDatabase" as SQL
component "Claims.ProcessorFn\n(Azure Functions)" as FN
component "Application Insights" as AI
component "Key Vault" as KV
queue "DLQ" as DLQ

U --> APIM
APIM --> API
API --> SBQ
SBQ --> FN
FN --> SQL

API --> AI
FN --> AI

API --> KV
FN --> KV

SBQ --> DLQ : poison msgs

@enduml

---

## Componentes principales
- **API Gateway**: Azure API Management (APIM)
- **API**: Azure App Service (.NET)
- **Procesamiento async**: Azure Functions (.NET)
- **Mensajería**: Azure Service Bus (Queue/Topic + DLQ)
- **Persistencia**: Azure SQL Database
- **Seguridad**: Key Vault + Managed Identity (fase 2)
- **Observabilidad**: Application Insights + Azure Monitor

---

## Qué demuestra (como Solutions Architect)
- Patrones enterprise: **command queue**, workers asíncronos, DLQ, reintentos e idempotencia (mínimo viable).
- Diseño y gobierno de APIs: gateway, políticas, versionado (según avance).
- Operación: señales mínimas, alertas, runbooks y troubleshooting orientado a incidentes.
- Decisiones documentadas: **ADRs**, diagramas C4 y NFRs.

---

## Roadmap v1 (MVP)
1) API publica comando a Service Bus
2) Function consume, procesa y actualiza estado en Azure SQL
3) DLQ habilitada + runbook de reproceso
4) App Insights + alertas mínimas
