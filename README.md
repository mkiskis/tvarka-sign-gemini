# Tvarka Sign for Gemini CLI

Official [Tvarka Sign](https://tvarka.eu/) extension for [Gemini CLI](https://geminicli.com/) and compatible Gemini agent environments.

Prepare PDF documents from Markdown, send documents for simple electronic signature (`esign`) or eIDAS qualified electronic signature (`qualified` via Smart-ID, Mobile-ID, or eID card/NFC), track signer progress, send workspace templates and Tvarka Formos requests, or sign a vault PDF yourself (`sign_now`).

## Install

```bash
gemini extensions install https://github.com/mkiskis/tvarka-sign-gemini
```

## Authentication

### 1. OAuth 2.1 sign-in (default)

The extension connects to `https://sign-api.tvarka.pro/mcp` over Streamable HTTP. On first use, Gemini CLI runs OAuth 2.1 discovery with PKCE (`S256`) and dynamic client registration, opening the Tvarka consent page in your browser where you select the workspace and approve access. No API key needs to be copied.

### 2. API key (`tvarka.eu` email workspaces or headless use)

To authenticate with a Tvarka API key (`tsk_live_...` or `tsk_test_...`) against `https://sign-api.tvarka.eu/mcp` or `https://sign-api.tvarka.pro/mcp`, configure `mcpServers` in `.gemini/settings.json`:

```json
{
  "mcpServers": {
    "tvarka-sign": {
      "httpUrl": "https://sign-api.tvarka.eu/mcp",
      "headers": {
        "X-Api-Key": "$TVARKA_API_KEY"
      }
    }
  }
}
```

## Available MCP tools

| Tool | Description |
|---|---|
| `create_document` | Render Markdown text to an A4 PDF/A in the workspace vault and return `documentId` and `previewUrl`. |
| `list_documents` | Search or list workspace vault documents available for signing. |
| `send_document` | Send a document (`markdown`, `pdfUrl`, `pdfBase64`, `file`, or `documentId`) to one or more signers (`level`: `qualified` or `esign`). |
| `request_signatures` | Start a signing ceremony on an existing vault `documentId`. |
| `get_signing` | Check per-signer status and retrieve `signedDocumentUrl` (and `evidenceUrl` for `esign`) once completed. |
| `list_signings` | List recent signings created through your connection or key. |
| `add_signer` | Add a signer to a pending qualified signing. |
| `remind_signer` | Re-send a signer's invitation email. |
| `cancel_signing` | Cancel a pending signing and retract outstanding invitations. |
| `list_templates` | List saved workspace templates and their role names. |
| `send_from_template` | Send a saved template by filling in role recipients. |
| `list_form_templates` | List published Tvarka Formos templates and their prefill fields. |
| `send_forms` | Send Tvarka Formos templates to a respondent by SMS or email. |
| `get_form_request` | Read the status, events, and submitted values of a form request. |
| `sign_now` | Sign a vault PDF yourself by Smart-ID or Mobile-ID on your phone. |
| `get_signature` | Poll a `sign_now` signature and retrieve `signedDocumentUrl` when completed. |

## Links

- Documentation (EU): https://sign-api.tvarka.eu/docs
- Documentation (LT / Pro): https://sign-api.tvarka.pro/docs
- Tvarka Sign (EU): https://tvarka.eu/
- Tvarka Sign (LT): https://sign.tvarka.pro/
- Privacy policy: https://tvarka.eu/privacy/
- Terms of service: https://tvarka.eu/terms/
- Support: info@tvarka.eu
