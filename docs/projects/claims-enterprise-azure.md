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
```mermaid
flowchart TB
  U[Usuario/Canal] --> APIM[Azure API Management]

  APIM --> API[Claims.Api<br/>(Azure App Service)]

  API --> SBQ[Service Bus Queue<br/>claims.commands]
  SBQ --> FN[Claims.ProcessorFn<br/>(Azure Functions)]
  FN --> SQL[Azure SQL Database]

  API --> AI[Application Insights]
  FN --> AI

  API --> KV[Key Vault]
  FN --> KV

  SBQ --> DLQ[(DLQ)]
```

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
