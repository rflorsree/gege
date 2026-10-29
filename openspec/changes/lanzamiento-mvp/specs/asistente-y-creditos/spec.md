# Spec Delta

## Purpose

Ofrecer respuestas del asistente a titulares de línea por web y WhatsApp con un cobro ligado a la entrega confirmada, recuperación ante fallos y límites de costo por empresa.

## ADDED Requirements

### Requirement: Bolsa mensual por línea
La plataforma SHALL asignar 100 créditos al plan básico y 300 al premium por periodo mensual de línea, y mostrar saldo disponible descontando reservas pendientes.

#### Scenario: Mensajes simultáneos con saldo limitado
- **WHEN** llegan dos solicitudes simultáneas y solo queda un crédito disponible
- **THEN** como máximo una obtiene reserva y la otra recibe una respuesta sin cargo por falta de saldo

### Requirement: Cobro único por respuesta
La plataforma SHALL reservar un crédito al iniciar una respuesta y confirmarlo una sola vez después de la entrega completa; en WhatsApp exige acuse `delivered` o `read`.

#### Scenario: Reintento de entrega o confirmación
- **WHEN** el canal o la API repiten el mismo identificador de respuesta
- **THEN** el libro de créditos conserva un solo débito para esa respuesta

#### Scenario: WhatsApp acepta pero no entrega
- **WHEN** WhatsApp confirma `sent` sin un acuse posterior `delivered` o `read`
- **THEN** el crédito permanece reservado hasta el plazo límite y luego se libera sin débito

### Requirement: Liberación ante fallo
La plataforma SHALL liberar la reserva si no se entrega una respuesta completa y deberá conciliar reservas que queden pendientes.

#### Scenario: Fallan modelo primario y alterno
- **WHEN** ambos modelos fallan antes de completar la respuesta
- **THEN** el titular recibe un aviso de indisponibilidad y no pierde un crédito

#### Scenario: Acuse tardío tras liberación
- **WHEN** llega `delivered` después de que venció y se liberó una reserva
- **THEN** la respuesta queda sin cargo y el evento se registra para conciliación

### Requirement: Contención de gasto
La plataforma SHALL limitar consumo de tokens y gasto por respuesta y aplicar una degradación acotada cuando se alcance el presupuesto diario de una empresa o el global.

#### Scenario: Aumento brusco de gasto
- **WHEN** el gasto del día alcanza el umbral de alerta o presupuesto configurado
- **THEN** se reducen recursos de IA para el ámbito afectado y siguen disponibles las consultas deterministas
