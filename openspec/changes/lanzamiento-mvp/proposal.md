# Proposal

## Why

Gege Tel necesita lanzar dos experiencias sobre una plataforma compartida en ocho semanas sin mezclar datos de empresas ni cobrar créditos incorrectamente. El equipo requiere un contrato de comportamiento y límites de arquitectura revisables antes de implementar.

## What Changes

- Habilitar gestión empresarial de líneas, centros de costo, consulta/descarga de facturas y solicitudes de corrección o cancelación.
- Publicar beneficios para titulares por web y WhatsApp con información de frescura.
- Ofrecer asistente de lectura con bolsa mensual de créditos por línea y cobro único por respuesta completada y entregada.
- Aislar datos y herramientas de IA por empresa y línea.
- Registrar fallos de proveedores, reconciliación y límites de gasto necesarios para un piloto.

Fuera de alcance inicial: pagos, cambios de plan desde el portal, herramientas de escritura del asistente, agentes múltiples y reemplazar sistemas de telefonía o timbrado.

## Capabilities

### New Capabilities

- `empresa-y-facturacion`: líneas, centros de costo, consulta de facturas y solicitudes de corrección/cancelación.
- `beneficios`: catálogo consultable por titulares con control de frescura.
- `asistente-y-creditos`: atención por web/WhatsApp, reservas, débitos y contingencia.
- `aislamiento-multiempresa`: acceso empresarial y de línea sin exposición cruzada.

### Modified Capabilities

Ninguna; el proyecto comienza sin especificaciones vigentes.

## Impact

Portal empresarial, web de titular, canal WhatsApp, API de negocio, sincronizadores de telefonía/catálogo/PAC, ejecutor de IA y PostgreSQL. Los contratos y supuestos pendientes están en el README.
