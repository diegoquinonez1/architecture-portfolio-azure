# Claims Enterprise (Azure)

## Objetivo general
Diseñar e implementar una plataforma de **gestión de reclamos (claims)** para seguros, orientada a integración enterprise en Azure, priorizando confiabilidad, trazabilidad y operación.

## Arquitectura (resumen)
- APIM → App Service (API) → Service Bus (commands/events) → Functions (workers) → Azure SQL
- Observabilidad: App Insights + alertas + runbooks
- Seguridad: Key Vault + Managed Identity (fase 2)

## Lo que demuestra
- Patrones async enterprise (DLQ, reintentos, idempotencia)
- Diseño de API gateway y políticas
- Decisiones documentadas (ADRs) y NFRs
