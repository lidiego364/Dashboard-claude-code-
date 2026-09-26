# Claude Code Dashboard — Guía en español

Este repositorio es una copia de [jspw/Claude-Code-Dashboard](https://github.com/jspw/Claude-Code-Dashboard),
importada con todo su historial de commits. Es una extensión de VS Code que muestra lo que Claude Code
hace en tu máquina: tokens usados, costo estimado, sesiones e insights de todos tus proyectos.

No necesita API key y no envía datos fuera de tu equipo: solo lee los logs locales en `~/.claude/projects/`.

> **Licencia:** AGPL-3.0 (ver [LICENSE](LICENSE)). Si modificas y distribuyes la extensión, debes
> publicar tu código bajo la misma licencia y mantener el crédito al autor original.

## Requisitos

- Node.js 20 o superior (probado con Node 22)
- VS Code 1.85 o superior
- [Claude Code](https://claude.ai/code) instalado y usado al menos una vez

## Instalar dependencias

```bash
npm ci
npm --prefix webview-ui ci
```

## Compilar y probar

```bash
npm run typecheck:all   # verificación de tipos (extensión + interfaz)
npm run test:all        # tests de la extensión y de la interfaz
npm run build           # genera dist/ y webview-ui/dist/
```

## Crear el instalable `.vsix` e instalarlo

```bash
npx vsce package --no-dependencies
code --install-extension claude-code-dashboard-*.vsix
```

Después de instalarla, reinicia VS Code y haz clic en el icono de **pulso** en la barra lateral.

## Desarrollo con recarga

1. Abre esta carpeta en VS Code.
2. En dos terminales ejecuta `npm run watch:ext` y `npm run watch:ui`.
3. Pulsa `F5` para abrir una ventana de VS Code con la extensión cargada.

## Qué incluye

| Pestaña | Contenido |
|---|---|
| **Overview** | Resumen semanal, tokens y costo de hoy, sesiones activas, lista de proyectos |
| **Charts** | Tendencia de tokens de 30 días, uso por proyecto, costo mensual proyectado |
| **Insights** | Mapa de calor, uso de herramientas, productividad por hora, archivos más editados |

Al hacer clic en un proyecto verás su historial de sesiones, la conversación turno a turno, el desglose
de tokens, los archivos tocados, su `CLAUDE.md` y los servidores MCP. Puedes exportar a JSON o CSV.

## Estructura del código

- `src/` — la extensión (lectura de sesiones, store, watchers, hooks, paneles)
- `webview-ui/` — la interfaz en React + Vite + Tailwind + Recharts
- `README.md`, `TECHNICAL.md`, `DATA_SOURCES.md` — documentación original en inglés
