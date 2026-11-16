# Installing the Enhancv MCP server

Enhancv is a **remote** MCP server hosted by Enhancv. There is nothing to clone, build or run locally, and no API key or environment variable to set.

## Configuration

Add this server to the MCP settings file:

```json
{
  "mcpServers": {
    "enhancv": {
      "type": "streamableHttp",
      "url": "https://api.enhancv.com/mcp"
    }
  }
}
```

- Transport: Streamable HTTP
- URL: `https://api.enhancv.com/mcp`

## Sign-in

The server uses OAuth 2.1 with PKCE and dynamic client registration. The first request without a token returns `401` with a `WWW-Authenticate` header that points to the protected resource metadata. The client then registers itself, and the user signs in to Enhancv in the browser and approves the connection. No credentials go in the configuration file.

The user needs an Enhancv account; sign-up is free at https://enhancv.com. On the free plan the tools can read resumes, cover letters and saved jobs and search jobs; editing and creating need a paid Enhancv plan.

## Verify

After sign-in, call `list_resumes`. It returns the user's resumes, which confirms the connection works.
