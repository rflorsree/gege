# Spec Delta

## Purpose

Dar a cada titular de línea acceso al catálogo de beneficios que le corresponde, indicando cuándo fue verificado frente al proveedor que no emite notificaciones de cambios.

## ADDED Requirements

### Requirement: Beneficios elegibles
La plataforma SHALL mostrar al titular autenticado únicamente los beneficios vigentes para su línea y plan según el último catálogo aceptado.

#### Scenario: Consulta por web o WhatsApp
- **WHEN** un titular consulta sus beneficios por un canal admitido
- **THEN** recibe la misma elegibilidad y fecha de actualización en ambos canales

#### Scenario: Línea ajena
- **WHEN** un titular intenta consultar beneficios de una línea vinculada a otra empresa
- **THEN** no recibe el catálogo privado ni información sobre la existencia de esa línea

### Requirement: Catálogo vencido
La plataforma SHALL señalar que el catálogo está desactualizado cuando se supera el umbral acordado sin una sincronización válida.

#### Scenario: Falla de consulta al proveedor
- **WHEN** falla la actualización del catálogo y ya venció su umbral de frescura
- **THEN** el titular ve un aviso de datos desactualizados y no se presenta un beneficio incierto como garantizado
