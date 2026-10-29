# Spec Delta

## Purpose

Mantener operables las funciones esenciales de Gege Tel ante fallos de un dominio de infraestructura o de un proveedor, sin perder ni duplicar efectos de procesos diferidos.

## ADDED Requirements

### Requirement: Continuidad ante un dominio caído
La plataforma SHALL distribuir las funciones esenciales entre dominios de fallo independientes y recuperar servicio tras la pérdida de uno de ellos.

#### Scenario: Pérdida de una zona o sitio
- **WHEN** deja de estar disponible un dominio que atiende solicitudes
- **THEN** otro dominio continúa o retoma el portal y la recepción de mensajes sin restaurar máquinas manualmente

### Requirement: Escalado independiente
La plataforma SHALL permitir aumentar por separado la capacidad de las APIs y los consumidores asíncronos sin guardar estado de sesión o trabajo solo en un proceso.

#### Scenario: Pico de mensajes
- **WHEN** crece el volumen de WhatsApp mientras el portal mantiene su carga habitual
- **THEN** se amplían los consumidores de mensajes sin duplicar efectos ni exigir escalar el portal en la misma proporción

### Requirement: Evento durable y procesable de nuevo
La plataforma SHALL conservar los trabajos asíncronos hasta su confirmación y permitir reintentos sin duplicar cambios de negocio.

#### Scenario: Consumidor cae después de ejecutar
- **WHEN** un consumidor termina una operación pero falla antes de confirmar el evento
- **THEN** el reintento reconoce la misma clave y no repite el débito ni la operación fiscal

### Requirement: Estado y publicación coherentes
La plataforma SHALL registrar en una misma transacción un cambio de negocio y la intención de publicar su evento correspondiente.

#### Scenario: Publicación temporalmente imposible
- **WHEN** el transporte de eventos no está disponible después del cambio confirmado
- **THEN** la intención permanece pendiente y se publica al recuperarse sin perder el cambio

### Requirement: Fallos visibles y recuperables
La plataforma SHALL exponer el atraso de colas, fallos repetidos y edad de los datos externos, y permitir revisar y reintentar trabajos apartados por error.

#### Scenario: Proveedor externo fuera de servicio
- **WHEN** un trabajo agota sus reintentos por indisponibilidad del proveedor
- **THEN** queda en estado recuperable, se alerta al operador y la interfaz muestra el estado pendiente o desactualizado

### Requirement: Restauración comprobada
La plataforma SHALL mantener copias recuperables de datos y practicar restauración y conmutación antes del piloto.

#### Scenario: Ensayo de recuperación
- **WHEN** se simula la caída de un dominio o la pérdida de un dato de prueba
- **THEN** el equipo documenta tiempo real de recuperación, pérdida observada y acciones pendientes frente a los objetivos acordados
