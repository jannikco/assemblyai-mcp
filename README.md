# AssemblyAI MCP server

Find existing transcripts and submit an authorized audio URL for asynchronous transcription, then poll completion.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `ASSEMBLYAI_API_KEY`



Credential help: https://www.assemblyai.com/docs/pre-recorded-audio/getting-started/transcribe-an-audio-file

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call assemblyai_list_transcripts '{"limit":5}'
```

## Use with an MCP client

Launch `node /absolute/path/assemblyai-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| assemblyai_list_transcripts | Read | assemblyai list transcripts |
| assemblyai_get_transcript | Read | assemblyai get transcript |
| assemblyai_submit_transcript | Explicit approval required | Submit an asynchronous transcription; poll get_transcript for completion. May consume provider credits. |

## Concrete workflow

Find existing transcripts and submit an authorized audio URL for asynchronous transcription, then poll completion.

1. assemblyai_list_transcripts
2. assemblyai_get_transcript
3. assemblyai_submit_transcript

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=assemblyai&integration=assemblyai-mcp&utm_source=github&utm_campaign=github-assemblyai-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/assemblyai/).

## Provenance and maintenance

- https://www.assemblyai.com/docs/openapi.json

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
