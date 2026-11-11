# HowdyGo MCP server

<img src="assets/icon.png" alt="HowdyGo" width="64" align="right" />

[HowdyGo](https://www.howdygo.com) turns recordings of your product into interactive demos. The HowdyGo MCP server connects your HowdyGo account to AI assistants (Claude, ChatGPT, GitHub Copilot, Codex, Cursor and others) so they can find, set up, edit, publish, share and export the demos in your library.

- **Server URL:** `https://app.howdygo.com/api/mcp`
- **Transport:** Streamable HTTP
- **Authentication:** OAuth. Your assistant asks you to sign in to HowdyGo when you connect. New users can start a free trial from the sign-in page.

This repository describes the hosted server and holds its client configuration. The server runs at the URL above; there's nothing to install or run locally.

## What you can do

- **Find demos:** search your library by title, folder or what a demo shows. Step text is searched too, so "the invoicing demo" works even if the title doesn't say so.
- **Set up a demo in one pass:** write step text from each recorded screen, auto-advance transitional clicks, add chapters, give the demo a descriptive title, and write the end-of-demo call to action and its background.
- **Rewrite for an audience:** rewrite the whole demo, or a single step, for sales, finance or a technical audience.
- **Edit the recorded screens:** change text on the captured pages (brand names, figures, sample data), and hide or blur sensitive elements.
- **Manage demos:** rename, duplicate, publish or unpublish a demo, and add, change or remove its viewer password.
- **Share:** get a demo's share link (on your custom domain if you have one) or its website embed code, inline or as a pop-up, and play published demos inline in the conversation.
- **Export:** export a demo as a GIF, WebM or MP4 file.
- **Answer questions about HowdyGo** from its documentation.

Your assistant can only reach the demos you can access, with your HowdyGo permissions. It asks before every change, and step edits save a version first, so changes can be restored from the demo's version history.

## Tools

| Tool | What it does |
| ---- | ------------ |
| `getAccount` | The connected HowdyGo account and organization |
| `searchDemos` | Find demos and sandboxes by title, folder or step text, with the step that matched |
| `getPublication`, `batchStepContext`, `getStepWithContext`, `getAnnotation` | Read a demo: its steps, its call to action, and each step's page and clicked element |
| `getStepScreenshot` | Screenshots of steps, with the click marked |
| `getElementContext`, `getPageStructure`, `getDomContext`, `getRawNode`, `getStepDiff` | Explore the recorded pages and what changed between steps |
| `searchPageText`, `listPageText` | Find the editable text on the recorded pages |
| `editDemo` | Edit step text, overlay labels and auto-advance, keyed by step number |
| `suggestTitle` | Rename a demo |
| `suggestChapter` | Add, rename or remove chapters |
| `suggestCtaContent`, `suggestCtaBackground` | Write the end-of-demo call to action and choose its background |
| `suggestAutoplay` | Turn autoplay on or off, and set its speed and looping |
| `suggestHtmlEdits` | Change text on the recorded pages |
| `suggestHideOrBlurElements` | Hide, blur or reveal elements on the recorded pages |
| `suggestDuplicateDemo` | Duplicate a demo |
| `suggestPublish` | Publish or unpublish a demo |
| `suggestPassword` | Add, change or remove a demo's viewer password |
| `getShareLink`, `getEmbedCode` | Get the share link, or the inline or pop-up embed code |
| `showDemo` | Play a published demo inline in the conversation |
| `exportDemo`, `getExport` | Export a demo as a GIF, WebM or MP4 file, and get its download link |
| `searchDocs`, `getDocsPage` | Answer questions from the HowdyGo docs |

## Setup

### Claude

1. Go to [Settings → Customize → Connectors](https://claude.ai/customize/connectors) and click **Add custom connector**.
2. Name it HowdyGo, paste the server URL, then click **Add**.
3. Click **Connect** and sign in to HowdyGo.

On Team and Enterprise plans, an Owner adds the connector under Organization settings → Connectors, then each member clicks Connect.

### ChatGPT

1. In ChatGPT on the web, go to [Plugins](https://chatgpt.com/plugins), click **+**, then **Add custom MCP server**.
2. Name it HowdyGo and paste the server URL under Connection.
3. Choose **OAuth** authentication, tick **I understand and want to continue**, then click **Create as a plugin**.
4. Install the plugin and sign in to HowdyGo. In a new chat, type **@** and pick HowdyGo.

On Business and Enterprise workspaces, only admins and owners can add custom MCP servers.

### GitHub Copilot in VS Code

Run **MCP: Add Server** from the Command Palette, choose **HTTP** and paste the server URL, or add it to `.vscode/mcp.json`:

```json
{
  "servers": {
    "howdygo": {
      "type": "http",
      "url": "https://app.howdygo.com/api/mcp"
    }
  }
}
```

Sign in to HowdyGo when VS Code asks.

### Claude Code

```sh
claude mcp add --transport http howdygo --scope user https://app.howdygo.com/api/mcp
```

Then run `/mcp` in Claude Code, choose howdygo and sign in.

### Codex

```sh
codex mcp add howdygo --url https://app.howdygo.com/api/mcp
```

Sign in to HowdyGo in the browser window that opens. If none opens, run `codex mcp login howdygo`.

### Cursor

Add it to `~/.cursor/mcp.json`, then sign in to HowdyGo when Cursor asks:

```json
{
  "mcpServers": {
    "howdygo": {
      "url": "https://app.howdygo.com/api/mcp"
    }
  }
}
```

### Other MCP clients

Add `https://app.howdygo.com/api/mcp` as a Streamable HTTP server and sign in with OAuth when your client asks.

## Try it

- "Which of my HowdyGo demos show the pricing page?"
- "Set up this demo: https://app.howdygo.com/edit/…" (paste one of your demo links)
- "Rewrite this demo for a sales audience."
- "On the recorded screens, replace Acme with Globex."
- "Export this demo as a GIF and give me the download link."
- "Give me the pop-up embed code for my newest demo."
- "Rename this demo to 'Invoicing walkthrough' and password-protect it."

New to HowdyGo? Record your first demo with the [HowdyGo Chrome extension](https://chrome.google.com/webstore/detail/interactive-screen-captur/kflpgokojhjknkikmnclhcpepnhgkcno), then ask your assistant to set it up.

## Support

- Documentation: [docs.howdygo.com](https://docs.howdygo.com)
- Email: [support@howdygo.com](mailto:support@howdygo.com)
- Privacy policy: [howdygo.com/legal/privacy-policy](https://www.howdygo.com/legal/privacy-policy)
- Terms: [howdygo.com/legal/terms-and-conditions](https://www.howdygo.com/legal/terms-and-conditions)
