# JARVIS Skills

Rust MCP server for JARVIS hardware, system, and file tools.

## Architecture

- **Runtime:** Rust (`tokio` + `axum`)
- **Transport:** HTTP JSON-RPC (`/jsonrpc`, `/mcp`) and stdio (`--stdio`)
- **Default bind:** `127.0.0.1:5050`
- **Tool catalog:** returned by `tools/list`, consumed by `jarvis-chat`

## Setup

```bash
cd jarvis-skills\rust-mcp-server
cargo build --release
```

## Run

HTTP mode:

```bash
cargo run --release
```

stdio mode (legacy, optional):

```bash
.\target\release\jarvis-rust-mcp-server.exe --stdio
```

## Verify implementation

Health:

```bash
curl http://127.0.0.1:5050/health
```

Tool list:

```bash
curl http://127.0.0.1:5050/tools
```

JSON-RPC tools/list:

```bash
curl -X POST http://127.0.0.1:5050/jsonrpc ^
  -H "Content-Type: application/json" ^
  -d "{\"jsonrpc\":\"2.0\",\"id\":\"1\",\"method\":\"tools/list\",\"params\":{}}"
```

## MCP client configuration

This repo includes:

- `.mcp.json`

- `.mcp.json` is STDIO command-based (recommended for Copilot CLI / Gemini CLI local testing).

Before using `.mcp.json`, build the Spotify server once:

```bash
cd ../spotify-mcp-server
npm install
npm run build
```

## Troubleshooting

- **Cannot connect to port 5050:** confirm no stale process holds the port and restart server.
- **Bluetooth toggle failures:** Windows may require elevated privileges for PnP operations.
- **Spotify commands:** use the standalone Spotify MCP server in `spotify-mcp-server` (https://github.com/wigglebop25/spotify-mcp-server).
