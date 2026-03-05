# Fraud Scoring Cloud-Native (AKS)

## Objetivo general
Diseñar e implementar una plataforma de **fraud/risk scoring (0–100)** para seguros, basada en microservicios en AKS y comunicación event-driven/streaming con Event Hubs.

## Arquitectura (resumen)
- APIM → AKS microservices
- Event Hubs para eventos
- PostgreSQL managed para persistencia y auditoría
- Observabilidad distribuida: OpenTelemetry + App Insights

## Lo que demuestra
- Decisiones cloud-native (AKS, escalado, resiliencia)
- Streaming vs mensajería
- Trazabilidad end-to-end y operación
