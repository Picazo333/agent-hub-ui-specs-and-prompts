# AgentHub — evaluación de propuesta visual de Google Stitch

**Fecha de revisión:** 2026-11-06 (CDMX). **Proyecto:** 001 / R08.
**Estado:** propuesta visual recibida; incorporación como guía de diseño evaluada. No se sustituye la implementación actual.
**Fuente:** exportación aportada por el alumno, `stitch_agenthub_admin_panel_prototype.zip`, que contiene `screen.png`, `code.html` y `DESIGN.md`.

## Comparación con `SPECS.md`

| Sección exigida | Evidencia de Stitch | Decisión |
| --- | --- | --- |
| Dashboard | Boceto visual con cuatro métricas ($5,200, $480, 3, 1), navegación, tabla de estado y placeholder del gráfico | Aprovechar solo referencias de densidad, jerarquía y tarjetas; mantener datos y comportamientos actuales |
| User Management | Entrada en el menú lateral, sin una vista implementada en el HTML exportado | Conservar la vista funcional del repositorio; no sustituirla |
| Agent Management | Entrada en el menú lateral; la tabla del Dashboard usa nombres y detalles diferentes a los del contrato | Conservar la vista funcional y los cinco agentes del `SPECS.md` |
| Skills | Entrada en el menú, sin catálogo ni interacciones en la exportación | Conservar catálogo y menús existentes |
| Agent Contracts | Entrada en el menú, sin tabla de contratos en la exportación | Conservar tabla, cálculo y modal existentes |
| Error Log | Entrada en el menú, sin tabla de errores ni operación de resolver | Conservar vista y acciones existentes |

## Riesgos concretos del HTML exportado

1. Es un boceto estático de Dashboard, no una implementación verificable de las seis vistas. No incorpora la lógica JavaScript de navegación, menús, modales, borrado ni marcado de errores.
2. El HTML utiliza atributos `style` y CSS embebido, en conflicto con las restricciones de la implementación del ejercicio.
3. Incluye controles y textos no acreditados por el contrato (por ejemplo, "Sync Data", "LIVE TELEMETRY" y actualización automática), que podrían inducir a creer que hay backend real.
4. En la captura se ven referencias de logotipo que no cargan. Los nombres de agentes en la tabla tampoco coinciden con los cinco nombres requeridos por `SPECS.md`.

## Decisión de incorporación

La propuesta de Stitch sirve como **guía de composición visual**, no como código de reemplazo. El proyecto ya implementaba la navegación y funcionalidades del contrato antes de esta generación. No se modifica el código solo por alinearlo con el boceto: hacerlo introduciría regresiones. Se conserva la versión funcional y se registran los elementos visuales estudiados. No se atribuye retrospectivamente a Stitch la autoría de la implementación previa.

**Pendiente para cerrar evidencia:** publicar los archivos originales del ZIP, especialmente `screen.png`, `code.html` y `DESIGN.md`, bajo esta misma carpeta; conservar prueba de que la especificación se utilizó como entrada en Stitch si la plataforma la ofrece. Verificar los archivos publicados en el PR #2. La prueba de funcionamiento/responsive del panel actual se evalúa en el QA final, no se infiere a partir del boceto.
