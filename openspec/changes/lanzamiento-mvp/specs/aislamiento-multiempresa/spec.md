# Spec Delta

## Purpose

Garantizar que portales, APIs y herramientas del asistente solo muestren o usen datos autorizados de la empresa y línea vinculadas a la identidad verificada.

## ADDED Requirements

### Requirement: Acceso empresarial autorizado
La plataforma SHALL resolver empresa y rol desde la sesión validada y comprobar permisos sobre cada recurso empresarial solicitado.

#### Scenario: Identificador de otra empresa
- **WHEN** un usuario solicita una línea o factura ajena por identificador directo
- **THEN** no recibe datos ni una señal que permita distinguir ese recurso de uno inexistente

### Requirement: Vínculo de titular vigente
La plataforma SHALL comprobar posesión del número y vínculo activo con la línea antes de mostrar beneficios, consumo o créditos al titular.

#### Scenario: Número reasignado
- **WHEN** la relación anterior entre número y línea deja de estar vigente
- **THEN** se revoca el acceso previo y el titular debe volver a verificarse

### Requirement: Herramientas de IA limitadas
La plataforma SHALL ofrecer al asistente solo herramientas autorizadas de consulta y verificará identidad, línea y empresa en cada ejecución.

#### Scenario: Instrucción maliciosa en un mensaje
- **WHEN** un mensaje solicita cambiar de empresa o consultar un recurso ajeno
- **THEN** la herramienta rechaza la operación y el asistente no revela el dato
