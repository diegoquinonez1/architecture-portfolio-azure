# Runbook: Triage de incidentes (v1)

## 1) Impacto
- ¿Qué está fallando? (API, processing, eventos)
- ¿A quién afecta? (usuarios, sistemas)
- ¿Se puede degradar funcionalidad?

## 2) Primeros checks (5 minutos)
- Disponibilidad del API (health endpoint)
- Errores 5xx y latencia p95 en Application Insights
- Dependencias: DB, Service Bus/Event Hubs
- Saturación (CPU/mem) si aplica

## 3) Mensajería / Eventos
### Service Bus
- Mensajes en DLQ
- Rate de procesamiento (consumo)
- Errores de lock/timeout

### Event Hubs
- Consumer lag (si lo expones)
- Errores de checkpointing
- Rate de eventos

## 4) Acciones típicas
- Reprocesar DLQ (paso a paso)
- Rollback/rollback deploy (si hay CI/CD)
- Mitigación temporal (throttling, feature flag)

## 5) Post-mortem (blameless)
- Causa raíz
- Acción correctiva
- Acción preventiva
- Lecciones aprendidas
