# Docmint MCP server

PDF and image tools for Claude, Claude Code, Cursor, VS Code, Windsurf and any MCP client: compress, merge, split,
rotate, protect, unlock, watermark, page numbers, OCR, extract text, convert to and from images, and more.

**Your files stay on your computer.** The server runs locally and reads and writes files on your machine. It only
contacts the Docmint API to count runs against your plan.

Full setup guide: https://docmint.io/mcp

## Add it to your app

Claude Code:

```bash
claude mcp add docmint -- npx -y docmint-mcp
```

Claude Desktop, Cursor (`~/.cursor/mcp.json`), Windsurf (`~/.codeium/windsurf/mcp_config.json`):

```json
{ "mcpServers": { "docmint": { "command": "npx", "args": ["-y", "docmint-mcp"] } } }
```

VS Code:

```bash
code --add-mcp '{"name":"docmint","command":"npx","args":["-y","docmint-mcp"]}'
```

Requires Node.js 20 or newer.

## Connect your Docmint account

Without an account you get 3 runs a day. Connect your account to use its plan (10 runs a day free, unlimited on Pro,
shared with the website):

```bash
npx -y docmint-mcp login
```

This opens the browser; approve the request while signed in. Or ask your AI app to "connect my Docmint account".
You can also paste a key from your account page: `npx -y docmint-mcp login dmk_…`, or set `DOCMINT_API_KEY`.

Other commands: `npx -y docmint-mcp status`, `npx -y docmint-mcp logout`.

Disconnect an app any time under **AI apps** on your Docmint account page.

## License

MIT. This covers the docmint-mcp package. The Docmint website and service have their own terms: https://docmint.io/terms
