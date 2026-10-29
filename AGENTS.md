# Guía breve para agentes

1. Leer `README.md`, `openspec/config.yaml` y el cambio `lanzamiento-mvp` antes de editar.
2. Ante decisiones que cambien alcance, límites de componentes, créditos o exposición de datos, presentar opciones y pedir decisión humana.
3. Escribir en español, con resultados verificables. No inventar contratos, precios, pruebas ni trazas de IA.
4. La API de negocio es la única puerta a datos empresariales. Sincronizadores y ejecutor de IA usan sus contratos; ningún agente recibe SQL, credenciales de base ni facultad de elegir `tenant_id`.
5. Cada cambio sigue OpenSpec: propuesta, requisitos, diseño si hace falta, tareas, revisión humana y aplicación. Una persona revisa seguridad multiempresa y créditos.
6. Este ejercicio es documental: no generar código, pseudocódigo, reglas de otros editores ni archivos de relleno.
