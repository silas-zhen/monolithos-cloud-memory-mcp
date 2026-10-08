# Monolithos Cloud Memory

Recall your authorized Monolithos Vault notes from an MCP-compatible AI assistant.
Keyword and hybrid search return original excerpts, Vault-relative source paths,
locators, and coverage information. Project filters are optional.

Publisher: **Monolithos, LLC** · [Website](https://monolithos.ai) ·
[Support](https://monolithos.ai/support.html)

## Connect

1. Enable Cloud Memory for your Vault in a Monolithos app version that supports
   this feature, and wait for the app to confirm the upload.
2. Add this remote MCP server to your assistant:

   ```text
   https://api.monolithos.ai/api/shadow/mcp
   ```

3. Complete the browser sign-in using your Monolithos account email, then review
   and approve the read-only memory permission for your Vault.
4. Ask the assistant to recall your notes and cite the returned sources.

The service uses Streamable HTTP and OAuth 2.0 with dynamic client registration
and PKCE. Users do not need to copy a token or an authorization code into this
plugin's configuration. The client completes its normal browser callback.
Installing the plugin does not upload a local Vault or authorize cloud sync.

### Cost and eligibility

The connector is free to install and use, with no separate connector fee or
purchase flow. It requires a Monolithos account and a Vault with Cloud Memory
enabled in the Monolithos app.

Monolithos subscriptions and AI allowances are managed at the platform level.
Trial users can also use this connector with their included AI allowance.
Hybrid search uses the account's existing query embedding allowance; keyword
search does not call an embedding provider.

### Cursor configuration

The repository includes a Cursor plugin manifest, `mcp.json`, and the official
Monolithos logo. A manual remote-server configuration is:

```json
{
  "mcpServers": {
    "monolithos-cloud-memory": {
      "url": "https://api.monolithos.ai/api/shadow/mcp"
    }
  }
}
```

Cursor discovers the OAuth flow from the server. No API key or client secret is
included in this repository. Directory submission and approval are separate
from installing a custom connection.

### Gemini CLI

Google has moved free and Google One consumer access to Antigravity CLI.
Gemini CLI remains available for supported enterprise licenses and paid API
access. See [Google's transition announcement](https://developers.googleblog.com/an-important-update-transitioning-gemini-cli-to-antigravity-cli/).
This extension targets Gemini CLI; the Monolithos connector itself is free.

Install the extension from this public repository:

```sh
gemini extensions install https://github.com/silas-zhen/monolithos-cloud-memory-mcp
```

Review and accept Gemini CLI's installation prompt, then start a new CLI session.
Complete the Monolithos browser sign-in and approve read-only access to your
chosen Vault. If the CLI shows that authentication is required, use:

```text
/mcp auth monolithos-cloud-memory
```

The root `gemini-extension.json` uses Streamable HTTP (`httpUrl`) and automatic
OAuth discovery. It contains no API key or client secret. Installation adds the
connection; it does not authorize access to a Vault by itself.

## Try it

- “Search my notes for a phrase using keyword mode and show original excerpts.”
- “Recall my design decisions about daylight and ventilation, with sources.”
- “What did we decide in the meeting? Cite the notes and identify anything unknown.”

The only tool is `monolithos_recall_memory`. Keyword mode searches indexed text;
hybrid mode also uses semantic evidence when available. Hybrid queries use the
account's query embedding allowance. Keyword queries do not call an embedding
provider.

Results are ranked by relevance. Date filtering is not currently supported.
Coverage may be partial, for example when a source cannot be read or has no
vector index. A zero-hit search does not prove that a note does not exist.

## Privacy and permissions

- Access is limited to the account and Vault authorized through OAuth.
- Sanctum private content is excluded from the cloud projection.
- This tool cannot edit or delete notes, or switch to another person's Vault.
- Cloud Memory is an optional service containing a synchronized projection;
  your local files remain in your Vault. Cloud processing is described in the
  feature's privacy notice.

[Cloud Memory privacy notice](https://monolithos.ai/cloud-memory-privacy.html) ·
[General privacy policy](https://monolithos.ai/privacy.html) ·
[Terms](https://monolithos.ai/terms.html) ·
[English demonstration](https://monolithos.ai/review/monolithos-mcp-20261008/)

## Help

If there are no results, check that Cloud Memory has confirmed an upload for the
same account and Vault. If authentication has expired, reconnect through your
assistant's normal connection settings. For help, contact **hello@monolithos.ai**.

The MIT license covers this repository's connection configuration and
documentation. The Monolithos name and logo remain the publisher's brand assets;
the license grants no trademark rights. This repository does not contain or
license the Monolithos application's or hosted service's private source code.
