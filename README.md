# mcp-todo-server

Servidor MCP (Model Context Protocol) de tareas pendientes, implementado con el
SDK oficial de TypeScript. Extraclase 1 — Model Context Protocol, Programación IV, UNA.

## Capacidades que expone

| Tipo     | Nombre           | Descripción                                              |
|----------|------------------|-----------------------------------------------------------|
| Resource | `tasks://list`   | Devuelve la lista completa de tareas (lee `tasks.json`)   |
| Tool     | `add_task`       | Agrega una tarea nueva (nombre, descripción, prioridad)   |
| Tool     | `complete_task`  | Marca una tarea como completada dado su `id`              |
| Prompt   | `daily_summary`  | Arma un resumen diario del estado de las tareas           |

## Instalación

```bash
npm install
npm run build
```

## Ejecución manual (modo stdio)

```bash
npm start
```

El servidor queda a la espera de mensajes JSON-RPC por stdin/stdout. No está
pensado para ejecutarse "suelto" en la terminal para uso normal: lo normal es
que un **cliente MCP** (Claude Desktop, MCP Inspector, etc.) lo lance como
subproceso.

## Probarlo con MCP Inspector (recomendado antes de conectar Claude Desktop)

```bash
npx @modelcontextprotocol/inspector node dist/server.js
```

Esto abre una interfaz web donde se puede ver el Resource, invocar los dos
Tools y probar el Prompt sin necesidad de un LLM real.

## Conectarlo a Claude Desktop

Agregar esta entrada en `claude_desktop_config.json` (ver sección de
configuración de Claude Desktop del sistema operativo correspondiente):

```json
{
  "mcpServers": {
    "todo-server": {
      "command": "node",
      "args": ["> mcp-todo-server@1.0.0 build"]
    }
  }
}
```

Reiniciar Claude Desktop por completo después de guardar el archivo.

## Estructura del proyecto

```
mcp-todo-server/
├── src/
│   └── server.ts      # Servidor MCP principal
├── tasks.json          # Almacenamiento de tareas (se crea/edita en tiempo de ejecución)
├── package.json
├── tsconfig.json
└── README.md
```
