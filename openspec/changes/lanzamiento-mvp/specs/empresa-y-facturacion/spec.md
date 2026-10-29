# Spec Delta

## Purpose

Permitir a cada empresa administrar líneas, centros de costo y facturas, incluidas solicitudes de corrección o cancelación, sin depender de la disponibilidad inmediata de proveedores externos.

## ADDED Requirements

### Requirement: Líneas y consumo visibles
La plataforma SHALL mostrar a un usuario empresarial autorizado las líneas de su empresa, su plan y el consumo obtenido de telefonía con fecha de última actualización.

#### Scenario: Datos externos atrasados
- **WHEN** la última sincronización de telefonía supera el umbral acordado
- **THEN** el portal muestra la fecha y un estado de datos desactualizados sin presentar el consumo como actual

### Requirement: Asignación a centro de costo
La plataforma SHALL permitir a un rol autorizado asignar una línea de su empresa a un centro de costo de esa misma empresa.

#### Scenario: Centro ajeno
- **WHEN** se intenta asignar una línea a un centro de costo de otra empresa
- **THEN** la operación se rechaza sin modificar la asignación ni revelar información del centro ajeno

### Requirement: Estado de factura
La plataforma SHALL permitir a un rol autorizado consultar y filtrar sus facturas por centro de costo, descargar XML/PDF disponibles y distinguir estados pendiente, timbrada, fallida y cancelada.

#### Scenario: PAC no disponible
- **WHEN** el PAC no confirma el timbrado
- **THEN** la factura permanece pendiente o fallida, con causa operativa y sin exhibir folio fiscal inexistente

### Requirement: Solicitud de corrección
La plataforma SHALL permitir a un rol autorizado solicitar la corrección de una factura propia y seguir el estado de la sustitución y cancelación del comprobante anterior.

#### Scenario: Corrección aún no confirmada
- **WHEN** se solicita corregir una factura y el PAC aún no confirma el CFDI sustituto o la cancelación anterior
- **THEN** el portal muestra el estado pendiente y conserva visibles ambos folios y su relación cuando existan

### Requirement: Solicitud de cancelación
La plataforma SHALL permitir a un rol autorizado solicitar la cancelación de una factura propia con motivo registrado y mostrar el resultado confirmado por el PAC.

#### Scenario: Cancelación pendiente de aceptación
- **WHEN** el PAC indica que la cancelación requiere aceptación del receptor
- **THEN** el portal mantiene la factura en estado de cancelación pendiente y no la presenta como cancelada
