# NFR Checklist (mínimo viable)

## Seguridad
- [ ] Autenticación definida (quién es el usuario/servicio)
- [ ] Autorización (RBAC/roles) definida
- [ ] Secretos fuera del código (Key Vault / GitHub Secrets)
- [ ] Cifrado en tránsito (TLS) y en reposo (DB/storage)
- [ ] Auditoría/logging de accesos relevante
- [ ] Principio de menor privilegio (least privilege)

## Resiliencia / Disponibilidad
- [ ] Timeouts y retries definidos (y dónde)
- [ ] Idempotencia en consumidores (mensajería/eventos)
- [ ] DLQ / poison messages manejados (si aplica)
- [ ] Objetivos RTO/RPO definidos (aunque sean estimados)
- [ ] Backups y restore probados/documentados

## Observabilidad / Operación
- [ ] Logs estructurados
- [ ] Correlation ID / trace propagation
- [ ] Métricas clave (errores, latencia p95, throughput)
- [ ] Alertas mínimas (errores, latencia, DLQ/lag, disponibilidad)
- [ ] Runbook de triage

## Performance / Escalabilidad
- [ ] Estrategia de escalado (autoscale / HPA / plan)
- [ ] Límites conocidos (cuellos de botella)
- [ ] Prueba simple de carga (mínimo)

## Costo (FinOps básico)
- [ ] Principales drivers de costo identificados
- [ ] Límites o presupuestos (budget) definidos en dev
- [ ] Estrategia de right-sizing (conceptual)
