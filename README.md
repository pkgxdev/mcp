# `pkgx` MCP

A [Model Context Protocol] server that can run any Open Source tool via
`pkgx`.

## Usage

1. Install [`pkgx`] (or not, we download it for you if you don’t)
2. `git clone https://github.com/pkgxdev/pkgx-mcp`
3. Consume in an MCP client (see below for configuration examples)

### Cursor/Claude Configuation

- `~/.cursor/mcp.json`:
- `~/Library/Application Support/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "pkgx": {
      "command": "/path/to/pkgx-mcp/main.ts"
    }
  }
}
```

Or without `pkgx`, but *with* `npx`:

```json
{
  "mcpServers": {
    "pkgx": {
      "command": "npx",
      "args": ["ts-node", "/path/to/pkgx-mcp/main.ts"]
    }
  }
}
```

### MCP Inspector

```sh
npx @modelcontextprotocol/inspector ts-node ./main.ts
```

## Suggested Prompts

```text
Use pkgx to run a series of git commands and generate statistics about this
repository.
```

## Security

Security? Hah.

But seriously, this is a dangerous tool. You are letting AI read any file on
your computer†. We have the decency to run `pkgx` in a sandbox so at least a
rogue AI can’t run `rm -rf /`. But we have not restricted reads because that
seemed too limiting.

We need the MCP protocol to advance to allow the user to be prompted with UI
to approve certain things that the AI cannot by itself do or something like
that.

In the meantime USE WITH ABSURD AMOUNTS OF CAUTION.

> † well, on macOS at least we prevent reads to `~/.ssh` and `~/.aws`, PRs
> welcome to exclude more and add Linux sandboxing.

> [!IMPORTANT]
>
> The AI cannot write to your file system.
>
> On macOS anyway. On Linux we need you to PR that for us.

[Model Context Protocol]: https://github.com/modelcontextprotocol
[`pkgx`]: https://pkgx.sh
