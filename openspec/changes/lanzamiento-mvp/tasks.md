# Tasks

La aplicación de estas tareas empieza tras revisar la propuesta y confirmar los supuestos abiertos. Todas están pendientes; esta entrega es de diseño.

## Semana 1 · Contratos y criterios

- [ ] Producto/UX confirma ciclo, plazo del acuse WhatsApp, elegibilidad, permisos de corrección/cancelación y estados de error con negocio.
- [ ] Integraciones obtiene contratos y límites reales de telefonía, catálogo, PAC y WhatsApp; registra incertidumbres.
- [ ] Plataforma e IA revisan especificaciones OpenSpec, diagramas y criterios de seguridad con el equipo.
- [ ] Infraestructura confirma si AWS y on premise cumplen los dominios de fallo, RTO/RPO y capacidad operativa requeridos; registra costos y dependencias.

## Semanas 2–3 · Base empresarial

- [ ] Plataforma implementa identidad, membresías, autorización y RLS; demuestra aislamiento entre dos empresas.
- [ ] Plataforma prueba outbox, publicación diferida, claves idempotentes y recuperación de eventos no confirmados.
- [ ] Producto/UX y plataforma entregan portal mínimo de líneas y centros de costo con datos de prueba.

## Semanas 3–5 · Datos y facturas

- [ ] Integraciones implementa sincronización idempotente de telefonía y catálogo, frescura visible y conciliación.
- [ ] Integraciones y plataforma integran timbrado, sustitución y cancelación PAC con motivos, estados pendientes y prueba de respuesta ambigua.
- [ ] Producto/UX entrega vínculo de titular y consulta web de beneficios, consumo y créditos.

## Semanas 5–6 · Asistente

- [ ] IA/canales integra WhatsApp y web, herramientas de lectura, deduplicación y acuses `delivered`/`read` fuera de orden.
- [ ] Plataforma e IA implementan reserva, débito al entregar, liberación y conciliación; prueban concurrencia, reintentos y acuses tardíos.
- [ ] IA/canales prueba alterno de modelo, topes de tokens y presupuesto sin afectar consultas deterministas.

## Semanas 7–8 · Aceptación y piloto

- [ ] Segunda persona revisa pruebas cruzadas de tenant, herramientas y logs, incluida inyección en texto de proveedor.
- [ ] Equipo ejecuta fallos controlados de proveedores, carga acotada y verificación de débito único.
- [ ] Infraestructura ensaya pérdida de una AZ o sitio, reintento y tópico de errores, conmutación de PostgreSQL y restauración de una copia; mide resultados contra RTO/RPO acordados.
- [ ] Producto decide piloto limitado, observa métricas y autoriza o recorta la salida según evidencia real.
