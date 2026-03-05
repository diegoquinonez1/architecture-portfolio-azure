# Skills Matrix (Azure Solutions Architect) — alineada al backlog (W1–W12)

Este documento conecta habilidades (prácticas reales) con evidencia en repos.

Repos:
- Claims (enterprise): https://github.com/diegoquinonez1/claims-enterprise-azure
- Fraud (cloud-native): https://github.com/diegoquinonez1/fraud-cloudnative-aks
- Portfolio (Pages): https://github.com/diegoquinonez1/architecture-portfolio-azure

---

## 1) Arquitectura y documentación
- **C4 (Context/Container) actualizado**
  - Evidencia:
    - `claims-enterprise-azure/docs/c4/` (W1 + actualización W4)
    - `fraud-cloudnative-aks/docs/c4/` (W7 + actualización W11)
    - `architecture-portfolio-azure/docs/projects/*.md` (resumen y mini-diagramas)
- **ADRs (decisiones con trade-offs)**
  - Objetivo:
    - ≥7 ADRs por repo (ideal 10)
  - Evidencia:
    - `claims-enterprise-azure/docs/adrs/0001-0007` (W1–W6)
    - `fraud-cloudnative-aks/docs/adrs/0001-0007` (W7–W12)
- **NFR checklist aplicado**
  - Evidencia:
    - `*/docs/nfr/nfr-checklist.md` con ítems marcados y notas de implementación

---

## 2) Integración (Enterprise vs Streaming)
- **Mensajería enterprise (Service Bus)**
  - Qué demostrar:
    - command queue / topic events, DLQ, reproceso, troubleshooting
  - Evidencia:
    - `claims-enterprise-azure` W2 (pub/consume) + W5 (DLQ demo + runbook)
    - `claims-enterprise-azure/docs/runbooks/incident-triage.md`
- **Event streaming (Event Hubs)**
  - Qué demostrar:
    - producer → consumer groups → pipeline de salida
  - Evidencia:
    - `fraud-cloudnative-aks` W9–W11 (eventos + consumers)

---

## 3) Datos (SQL transaccional vs Postgres operacional)
- **Azure SQL (transaccional / estados de claim)**
  - Evidencia:
    - `claims-enterprise-azure` W3 (EF Core + schema + estados)
    - ADR de data store (Azure SQL)
- **PostgreSQL managed (features + scoring + auditoría)**
  - Evidencia:
    - `fraud-cloudnative-aks/docs/contracts/postgres-schema-v1.sql` (W9)
    - `fraud-cloudnative-aks/docs/contracts/feature-queries-v1.sql` (W10)
    - `fraud-cloudnative-aks` tablas: `processed_events`, `fraud_scores`

---

## 4) Reliability / Resiliencia operable
- **Idempotencia**
  - Evidencia:
    - `claims-enterprise-azure` (W3–W5) idempotencia mínima en consumer
    - `fraud-cloudnative-aks` (W10–W11) tabla `processed_events` + dedupe por `(consumer_name, event_id)`
- **Manejo de fallos**
  - Service Bus:
    - DLQ + reproceso documentado (W5)
  - Event Hubs:
    - estrategia documentada (replay, dedupe, checkpoints) (W10–W12)
- **Timeouts/retries**
  - Evidencia:
    - ADR o doc de resiliencia + implementación básica en servicios (cuando aplique)

---

## 5) Observabilidad (mínimo viable y distribuida)
- **Enterprise**
  - Evidencia (W5):
    - App Insights para API + Functions
    - Correlation ID end-to-end
    - 3–5 alertas documentadas
- **Cloud-native**
  - Evidencia (W11–W12):
    - OpenTelemetry + App Insights
    - 1 trace end-to-end (ingestion → feature → scoring)
    - alertas + runbook actualizado

---

## 6) Seguridad (por fases)
- **Auth MVP**
  - Evidencia:
    - APIM con subscription key + rate limiting (W4 claims, W12 fraud)
- **Auth enterprise (fase 2)**
  - Evidencia:
    - ADR + diseño: Entra ID (OAuth/OIDC) + `validate-jwt` en APIM
- **Secret management**
  - Evidencia:
    - Key Vault + (ideal) Managed Identity, o plan documentado si queda para fase 2

---

## 7) Infra as Code y CI/CD
- **IaC**
  - Evidencia:
    - `claims-enterprise-azure/infra/bicep/` (W6)
    - `fraud-cloudnative-aks/infra/terraform/` (W8–W10)
- **CI**
  - Evidencia:
    - `.github/workflows/ci.yml` en ambos repos (build/test en PR + main)
- **Deploy automático (opcional, no bloquear MVP)**
  - Evidencia:
    - workflows presentes pero puedes dejarlos manuales hasta que entiendas OIDC

---

## 8) Evidencia por semana (resumen rápido)
- **W1–W6 (claims-enterprise-azure)**: base docs + Service Bus + Azure SQL + APIM/KV + observabilidad + Bicep
- **W7–W12 (fraud-cloudnative-aks)**: AKS + Terraform + Event Hubs + Postgres + features reales + scoring + OTel + APIM + demo
- **Portfolio continuo**: `docs/projects/*` + links a evidencia + (opcional) weekly log

---

## 9) Plan para “fase 2” 
- Entra ID completo (OAuth/OIDC) — ADR + diagrama, implementación después
- Private networking avanzado — NFR + ADR
- OIDC GitHub Actions deploy automático — workflows listos, habilitar después
