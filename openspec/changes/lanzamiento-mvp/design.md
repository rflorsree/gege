# Design

## Context

Dos productos comparten líneas, identidad, beneficios, facturación y créditos. El equipo tiene cuatro personas y ocho semanas. Los proveedores externos pueden entregar datos tarde o fallar. La arquitectura y dos diagramas de flujo se explican en el [README principal](../../../README.md).

## Decisions

1. **Tres componentes desplegables.** API de negocio, sincronizadores de proveedores y ejecutor de IA. Portal empresarial y web de titular son clientes separados. La API posee todos los datos empresariales y ofrece contratos a los otros componentes. Así pueden escalar y fallar por separado sin introducir un servicio y base por cada función.
2. **Una base, un dueño de acceso.** PostgreSQL sirve al MVP y solo la API de negocio abre conexiones. Cada fila empresarial se identifica por `tenant_id`. La API valida sesión, empresa, rol y recurso; RLS protege también consultas omitidas accidentalmente. El rol de aplicación carece de privilegios de bypass y las migraciones usan otro rol. El contexto de tenant se fija dentro de cada transacción, nunca en una conexión reutilizada.
3. **Integraciones por contratos idempotentes.** El sincronizador consulta telefonía y catálogo con cursores o marcas de tiempo disponibles y entrega a la API cambios normalizados con clave de proveedor. La API registra última actualización, errores y versión de origen. Para PAC, conserva estado pendiente hasta confirmar timbrado, corrección o cancelación y concilia respuestas ambiguas antes de repetir operaciones. La corrección relaciona CFDI sustituto y anterior; una cancelación registra motivo y puede requerir aceptación del receptor.
4. **Asistente con herramientas de lectura.** Web y WhatsApp se normalizan a una identidad de línea validada. El modelo solo propone llamadas a beneficios, consumo y saldo; la API autoriza cada llamada. Se separan instrucciones de sistema de texto del usuario y proveedor. No hay acceso directo a base, web abierta, herramientas de escritura, memoria entre empresas ni agentes múltiples.
5. **Créditos como libro transaccional.** La API reserva bajo bloqueo o actualización condicional del saldo para un ID de respuesta único. Reserva y débito pertenecen al mismo periodo de la línea. Web confirma la respuesta completa; WhatsApp confirma solo con `delivered` o `read` asociado al ID saliente. `sent` no cobra. Un fallo previo o el vencimiento libera; un acuse tardío no vuelve a cobrar. La conciliación resuelve reservas vencidas, eventos duplicados y estados inciertos.
6. **Contingencia y costo.** El ejecutor aplica límites de tokens, duración y gasto. Una falla del modelo permite un intento con alterno solo en operaciones de lectura y con la misma reserva. El presupuesto absoluto y la comparación contra gasto habitual activan degradación por empresa/canal antes de un corte global. Las consultas deterministas siguen operando.

## Trust boundaries

| Límite | Validación al cruzarlo |
| --- | --- |
| Navegador empresarial → API | Sesión, membresía, rol, recurso y tenant. |
| Web/WhatsApp → ejecutor | Identidad de canal, deduplicación y vínculo de línea vigente mediante API. |
| Ejecutor/sincronizador → API | Identidad de servicio y operación permitida; nunca tenant libre elegido por modelo o evento. |
| API → PostgreSQL | Rol restringido, transacción con contexto de tenant, RLS, auditoría. |
| Proveedores → plataforma | Autenticidad, esquema esperado, límites, idempotencia y marcas de frescura. |

## Alternatives and consequences

- Bases propias por componente darían independencia de datos, pero añadirían sincronización distribuida y más operación antes del piloto. Se reconsideran si aparecen equipos y ciclos de despliegue realmente independientes.
- Un único proceso para todo simplificaría despliegue, pero acoplaría picos de IA y caídas de proveedores con el portal. Los tres componentes acordados aíslan estos fallos.
- Cobrar por token trasladaría variación de modelo al cliente y dificultaría entender la bolsa mensual. Se acordó un crédito por respuesta completada; el costo variable se controla internamente.

## Open questions

Validar con negocio el ciclo mensual, prorrateo, plazo máximo de reserva, expiración del catálogo y permisos para corregir/cancelar. Validar con PAC/SAT las reglas fiscales concretas y con el BSP la disponibilidad de `delivered`/`read`, reintentos, orden de eventos y retención. Estas respuestas pueden modificar la especificación antes de implementar.
