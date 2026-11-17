<p align="center">
  <img src="assets/enhancv-logo.png" alt="Enhancv" width="96" height="96">
</p>

<h1 align="center">Enhancv MCP Server</h1>

<p align="center">
  Let Claude, ChatGPT, Cursor and other AI apps edit your <a href="https://enhancv.com">Enhancv</a> resumes and cover letters, search jobs and update your job tracker. Changes show up live in the Enhancv editor.
</p>

<p align="center">
  <a href="https://claude.ai/directory/enhancv">Add to Claude</a> ·
  <a href="https://cursor.com/install-mcp?name=enhancv&config=eyJ1cmwiOiJodHRwczovL2FwaS5lbmhhbmN2LmNvbS9tY3AifQ%3D%3D">Add to Cursor</a> ·
  <a href="https://vscode.dev/redirect?url=vscode%3Amcp%2Finstall%3F%257B%2522name%2522%253A%2522enhancv%2522%252C%2522type%2522%253A%2522http%2522%252C%2522url%2522%253A%2522https%253A%252F%252Fapi.enhancv.com%252Fmcp%2522%257D">Add to VS Code</a> ·
  <a href="https://help.enhancv.com/en/articles/18458503-connect-enhancv-to-claude-chatgpt-and-other-ai-apps">Docs</a>
</p>

---

This is Enhancv's official **remote MCP server**. It's hosted by Enhancv, so there's nothing to install or run: point your AI app at the URL below and sign in with your Enhancv account.

```
https://api.enhancv.com/mcp
```

- **Transport:** Streamable HTTP
- **Auth:** OAuth 2.1 with PKCE. You sign in to Enhancv and approve the connection. Supports dynamic client registration and client ID metadata documents.
- **MCP Registry:** [`com.enhancv/mcp`](https://registry.modelcontextprotocol.io/v0.1/servers?search=com.enhancv)

This repository holds the server's documentation; the server itself runs on Enhancv's infrastructure.

## What you can do

- **Tailor a resume to a job.** Your AI reads your resume and a job ad, then rewrites the summary, bullets and skills in place, keeping every fact true to your experience.
- **Edit and restyle resumes.** Rewrite fields and bullet lists, add or remove entries, add, delete and reorder sections, and change the template, font and spacing.
- **Manage resumes.** List, read, create, duplicate and import resumes, and download any resume as a PDF.
- **Write cover letters.** Write a cover letter from your resume and attach it to a job you saved.
- **Find and track jobs.** Search Enhancv's job feed, save jobs to your job tracker, update their status and add notes.

If the resume is open in the Enhancv editor, you see each change appear as your AI makes it, and you can keep or undo it.

## Setup

### Claude (web, desktop and mobile)

1. Open [Enhancv in Claude's connector directory](https://claude.ai/directory/enhancv).
2. Select **Connect**, sign in to Enhancv and allow the connection.

If your Claude organization doesn't allow directory connectors, add it as a custom connector instead: open [Claude's connector settings](https://claude.ai/customize/connectors) and add a custom connector with the URL `https://api.enhancv.com/mcp`.

### ChatGPT

1. Open [ChatGPT's plugin settings](https://chatgpt.com/plugins).
2. Add a custom connector with the URL `https://api.enhancv.com/mcp`.
3. Sign in to Enhancv and allow the connection.

### Claude Code

```bash
claude mcp add --transport http --scope user enhancv https://api.enhancv.com/mcp
```

### VS Code

Use the **Add to VS Code** link above, or run:

```bash
code --add-mcp '{"name":"enhancv","type":"http","url":"https://api.enhancv.com/mcp"}'
```

### Cursor

Use the **Add to Cursor** link above, or add this to your `mcp.json`:

```json
{
  "mcpServers": {
    "enhancv": {
      "url": "https://api.enhancv.com/mcp"
    }
  }
}
```

### Any other MCP client

Add a remote MCP server (Streamable HTTP) with the URL `https://api.enhancv.com/mcp`. The client will open Enhancv's sign-in the first time you use it.

You can also find one-click setup for each app in Enhancv under **Account → AI connections**.

## Tools

| Tool | What it does | Scope | Type |
|---|---|---|---|
| `list_resumes` | List your resumes, most recently edited first | `resumes:read` | Read |
| `get_resume` | Read a resume or cover letter in full, with the IDs the edit tools use | `resumes:read` | Read |
| `download_resume` | Render a resume or cover letter as a PDF and return its link | `resumes:read` | Read |
| `list_cover_letters` | List your cover letters and the saved job each is linked to | `resumes:read` | Read |
| `list_saved_jobs` | List the jobs in your job tracker with their status | `resumes:read` | Read |
| `get_saved_job` | Read a saved job with its full description and your notes | `resumes:read` | Read |
| `search_jobs` | Search Enhancv's job feed | `resumes:read` | Read |
| `edit_field` | Change one field of a resume | `resumes:write` | Write |
| `edit_multiple_fields` | Change several fields at once | `resumes:write` | Write |
| `edit_list` | Rewrite a bullet list | `resumes:write` | Write |
| `add_item` | Add an entry to a section | `resumes:write` | Write |
| `remove_item` | Remove an entry from a section | `resumes:write` | Write |
| `add_section` | Add a section | `resumes:write` | Write |
| `delete_section` | Delete a section | `resumes:write` | Write |
| `move_section` | Move a section, as dragging it in the editor does | `resumes:write` | Write |
| `move_item` | Reorder an entry within its section | `resumes:write` | Write |
| `create_resume` | Create a new, blank resume | `resumes:write` | Write |
| `duplicate_resume` | Copy a resume, e.g. before tailoring it to a job | `resumes:write` | Write |
| `import_resume` | Make an Enhancv resume from resume text you share | `resumes:write` | Write |
| `create_cover_letter` | Save a cover letter, optionally linked to a saved job | `resumes:write` | Write |
| `save_job` | Add a job to your job tracker | `resumes:write` | Write |
| `update_saved_job` | Change a saved job's details or status, or add a note | `resumes:write` | Write |

Every edit takes the resume's current version. If you changed the resume in the meantime, nothing is overwritten: the tool returns the latest version so your AI can read it and try again.

## Example prompts

- "Tailor my latest resume to this job description: …"
- "Rewrite the bullets in my most recent role to show impact with numbers."
- "Find remote product designer jobs and save the best three to my job tracker."
- "Write a cover letter for the job I saved at Acme and link it to that job."
- "Duplicate my resume as 'Data Analyst version', switch it to a one-column template and download the PDF."

## Plans

- **Free Enhancv plan:** your AI can read your resumes, cover letters and saved jobs, and search jobs.
- **Paid Enhancv plans:** your AI can also edit, create, import and download resumes, write cover letters and update your job tracker.

## Privacy and security

- You sign in to Enhancv and approve the connection yourself. Your AI app never sees your Enhancv password.
- The connector only reaches your own resumes, cover letters and saved jobs. It can't delete resumes or saved jobs, and it has no access to your account settings or billing.
- Disconnect any AI app at any time in Enhancv under **Account → AI connections**. It loses access immediately.
- Rate limits: 60 calls per minute and 1,000 per hour per user.

Read our [privacy policy](https://enhancv.com/privacy/#ai-connections) and [terms](https://enhancv.com/terms/).

## Support

- Docs: [Connect Enhancv to Claude, ChatGPT and other AI apps](https://help.enhancv.com/en/articles/18458503-connect-enhancv-to-claude-chatgpt-and-other-ai-apps)
- Email: [help@enhancv.com](mailto:help@enhancv.com)
- Issues with this documentation: open an issue in this repository.

---

Enhancv and the Enhancv logo are trademarks of Enhancv. The text in this repository is licensed under the [MIT License](LICENSE).
