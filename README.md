# MyPetDance MCP server

Read-only MCP server for [MyPetDance](https://mypetdance.com/), AI trend video templates for pets: upload a photo of your dog or cat and get the viral dance or meme video back with your pet in it.

Ask your AI assistant things like "which template is the End of Watch meme and how much does it cost?" and it can look the answer up here instead of guessing.

- Endpoint: `https://mypetdance.com/mcp` (Streamable HTTP)
- No API key, no sign-in
- Read-only: it lists templates and prices, it can't make videos or touch accounts

It is also listed in the official MCP Registry as `com.mypetdance/templates`.


## Tools

| Tool | What it returns | Arguments |
|---|---|---|
| `search_templates` | Search templates by meme name, alias or keyword. Each result has the page link, how many photos to upload, lengths and credit prices. Empty query lists everything. | `query`, `limit`, `offset` |
| `get_template` | Full details of one template by slug (e.g. `cat-riding-surron-ai`), id or page URL, including its guide pages. | `slug` |
| `get_pricing` | Credit packs and prices in US dollars. | none |

## Connect

**Claude Code**

```bash
claude mcp add --transport http mypetdance https://mypetdance.com/mcp
```

**Claude Desktop, Cursor, Windsurf and other clients** that take a JSON config:

```json
{
  "mcpServers": {
    "mypetdance": {
      "url": "https://mypetdance.com/mcp"
    }
  }
}
```

Clients that only speak stdio can go through [mcp-remote](https://www.npmjs.com/package/mcp-remote):

```json
{
  "mcpServers": {
    "mypetdance": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mypetdance.com/mcp"]
    }
  }
}
```

## Try it with curl

```bash
curl -s https://mypetdance.com/mcp \
  -H 'content-type: application/json' \
  -H 'accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_template","arguments":{"slug":"cat-riding-surron-ai"}}}'
```

The same data is available as plain JSON at `https://mypetdance.com/api/v1/templates`.

## About this repo

The server runs on mypetdance.com itself; this repo only holds the docs and `server.json`. Questions or problems: open an issue.

## License

MIT
