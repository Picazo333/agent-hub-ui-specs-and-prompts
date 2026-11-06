# AgentHub Admin Panel

Prototipo estático del panel de administración interno de AgentHub. AgentHub es una plataforma donde las empresas alquilan agentes de IA con skills. Esta pantalla es para el administrador interno: ingresos, usuarios, agentes, catálogo de skills, contratos y errores de ejecución.

No hay backend ni conexión a una API. Todos los registros están escritos en `index.html` y coinciden con `SPECS.md`.

## Cómo ejecutarlo

Hace falta Python 3. Con el servidor incluido en la plantilla [html-hello](https://github.com/4GeeksAcademy/html-hello):

```bash
pip3 install flask
python3 server.py
```

Abrir `http://127.0.0.1:3000`.

También se puede servir la carpeta con el servidor estático de Python:

```bash
python3 -m http.server 3000
```

Tailwind se carga desde `https://cdn.tailwindcss.com`, así que la página necesita red la primera vez.

## Estructura

| Archivo | Uso |
| --- | --- |
| `SPECS.md` | Contrato del prototipo: producto, stack, datos, interacciones y criterios de aceptación. Se escribió antes del HTML. |
| `index.html` | Panel completo: seis secciones, estilos Tailwind y JavaScript vanilla. |
| `server.py` | Servidor local de la plantilla html-hello. El HTML de reserva ya no usa atributos `style`. |
| `learn.json` | Metadatos del proyecto. |
| `.vscode/` | Ajustes y asset de la plantilla html-hello. |

## Decisiones técnicas

- Un solo `index.html`. La navegación cambia el hash y muestra una sección. No recarga la página, así el modo claro u oscuro se mantiene al pasar de una sección a otra.
- Tailwind solo por CDN, con `darkMode: 'class'`. No hay archivo CSS ni atributos `style`.
- El modo oscuro añade la clase `dark` en `<html>` y los colores usan utilidades `dark:`. La elección se guarda en `localStorage` (`agenthub-theme`). La primera visita sigue `prefers-color-scheme`.
- Escape cierra el modal, si no hay modal el menú abierto, y si no el sidebar móvil.
- Los menús `⋮` se mueven al final de `body` mientras están abiertos y se colocan con clases de Tailwind, para que el scroll horizontal de las tablas no los recorte.
- Las listas de skills de cada agente empiezan colapsadas. Abrirlas anima `grid-template-rows` durante 300 ms.
- Eliminar una fila y marcar un error como resuelto cambian solo la página actual. El texto del system prompt se conserva en la sesión si se edita y se vuelve a abrir Configure.
- Los mismos agentes (Atlas Research, Ledger Clerk, Inbox Triage, Field Notes y Compliance Watch) aparecen en gestión de agentes, contratos y log de errores.

El enunciado sugiere usar Google Stitch como referencia visual a partir de `SPECS.md`. Esta entrega no envió la especificación a Stitch ni a otro servicio externo. La interfaz se construyó directamente desde `SPECS.md`.
