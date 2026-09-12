# ettu plugins

Install ettu's MCP connection and skills together. Create characters, switch live status, claim @handles, follow users and characters, and take photos, organize albums and follow activity and photo notifications through your AI.

**Website:** [ettu.lol](https://ettu.lol) · **MCP endpoint:** `https://ettu.lol/mcp` · **Bundle:** 0.16.2

Use [ettulol/ettu-plugins](https://github.com/ettulol/ettu-plugins) when your AI app asks for a **marketplace repository**. Use `https://ettu.lol/mcp` when it asks for an **MCP server URL**. The hosted service runs on ettu; users install only configuration and skills, then sign in with their own approved ettu account. No local server or API key is needed.

Read the [MCP contract](docs/mcp/README.md) for the 70 tools, scopes and workflows, or [release notes](plugins/ettu/release.json) for changes.

## Install in Codex

Run:

```sh
codex plugin marketplace add https://github.com/ettulol/ettu-plugins
codex plugin add ettu@ettu-plugins
```

If Codex asks for a marketplace repository URL, provide the same **repository URL**, then install **ettu** from **ettu-plugins**. Do not provide a raw JSON URL, a link to `plugins/ettu`, or the MCP service URL in that repository field.

Start a new Codex conversation after installing. Complete ettu OAuth sign-in when prompted. Ask “Show my ettu characters” as a read-only check. The skill is bundled and available across projects on the host where the plugin is installed; no per-project skill copy is needed. Enable it on other hosts separately. Generic character brainstorming does not request publication on ettu.

These commands are available in current Codex CLI versions; check `codex plugin --help` if your version differs. For the plugin browser, open `/plugins`. See [OpenAI plugin usage](https://learn.chatgpt.com/docs/plugins).

## Install in Claude Code

Run inside Claude Code:

```text
/plugin marketplace add https://github.com/ettulol/ettu-plugins
/plugin install ettu@ettu-plugins
```

Choose **user** scope to use it across your projects. Follow the install summary if it asks you to reload plugins, or start a new session. Open `/mcp` and authenticate the ettu connection. Ask “Show my ettu characters”; `/ettu:ettu` explicitly invokes the bundled skill.

The two catalogs point to the same `plugins/ettu` directory. Claude reads `.claude-plugin/marketplace.json`; Codex reads `.agents/plugins/marketplace.json`. See [Claude marketplace documentation](https://code.claude.com/docs/en/plugin-marketplaces).

## ChatGPT and Claude — coming soon

New connections are currently guided through **Codex** and **Claude Code**. ChatGPT and Claude setup is **Coming soon**. Existing authenticated MCP connections continue to work; this does not revoke access or remove installed connections. [ChatGPT integration notes](docs/chatgpt.md) remain available for maintainers and existing installations.

## What you can do

- Create a character in Clay, Anime or Vintage with a personality, appearance, voice direction, a name of up to 100 characters, and 3–50 favorites and hates each. Universe selection is permanent.
- Browse public characters, photos and creator profiles. Request existing character portraits or sprite sheets as inline PNGs and download links, or retrieve GIFs and manifests.
- Review a new character’s private first look: approving it publishes that picture immediately, with optional angles and a face portrait following in the background. Updates to existing characters stay private until explicitly published.
- Generate fresh artwork from unchanged character details, or retry a failed private version under the same version number. Archive characters and delete unreferenced characters after confirming their exact name.
- Set live moods and activities independently of revisions. Status GIFs generate on first use, with idle artwork displayed while they are pending.
- Choose a main character, set your public name and @handle, and follow creators or characters. Ask “Open my profile” for your link; your signed-in profile also contains settings and connected assistants.
- Take a selfie or invite a group from the same universe. Accept photo invitations with a pose. The creator reviews a private preview and chooses “I like it” to publish it; then organize approved photos in private albums.

The `ettu` skill is optional for MCP access: a connected AI can discover the server tools automatically. The bundle adds interview, character publication and photo invitation guidance plus the `ettu-update` skill.

## Check for updates

Ask **“Check for ettu updates”**. The bundled `ettu-update` skill reports your installed version, the latest available version, relevant changes, and how to update in your AI app. In Claude Code, `/ettu:ettu-update` invokes it explicitly.

The remote MCP service updates on the server. Local skills and connection configuration update when your host installs a new plugin bundle, including its `release.json`. Refreshing the marketplace catalog alone is not the same as updating the installed plugin. Checking is read-only; it does not automatically install anything. An unreachable release source is reported as an unverified check.

For an existing Codex Git marketplace installation:

```sh
codex plugin marketplace upgrade ettu-plugins
codex plugin add ettu@ettu-plugins
```

For Claude Code:

```text
/plugin marketplace update ettu-plugins
/plugin update ettu@ettu-plugins
/reload-plugins
```

Start a new Codex conversation, or follow your host's reload instructions. Keep your existing installation source and scope. For managed workspaces or uploaded ZIPs, use the installation surface's update process. See the [host update guide](plugins/ettu/skills/ettu-update/references/update-host.md).

The installed `release.json` records the version on disk. Its `latest_manifest_url` checks this repository's default branch for the latest release, using the GitHub contents API with `Accept: application/vnd.github.raw+json`. Release notes travel with each bundle so older installations can explain what changed. No installer scripts or GitHub tokens are needed.

## Connection help

- If ettu requests an invitation, use [the waitlist](https://ettu.lol/waitlist). Requests and invitations are handled by Clerk; joining the waitlist does not grant access yet.
- For missing tools, enable the ettu connection, finish OAuth sign-in and refresh tools or start a new conversation. Typical authoring needs both read and write permissions.
- Manage authorized assistants from your signed-in profile; [account](https://ettu.lol/account) redirects there. Revoking a connection requires that assistant to authorize again.
- If `ettu.lol` cannot resolve or the endpoint is unavailable, the connection cannot finish until the hosted service is reachable. Changing a skill or supplying a personal API key will not fix that.

## Repository layout

```text
.agents/plugins/marketplace.json     Codex catalog
.claude-plugin/marketplace.json      Claude catalog
docs/mcp/README.md                  Public MCP contract and tool inventory
docs/mcp/contract.json              Exact tool schemas and scopes
plugins/ettu/
  .codex-plugin/plugin.json          Codex manifest
  .claude-plugin/plugin.json         Claude manifest
  .mcp.json                         Shared endpoint configuration
  release.json                      Bundle version and release notes
  assets/ettu-icon.png               Yellow ettu plugin icon
  skills/*/agents/openai.yaml        Skill branding metadata
  skills/*/assets/ettu-icon.png      Self-contained skill icons
  skills/ettu-update/SKILL.md        Update check and guidance
  skills/ettu-update/references/update-host.md
  skills/ettu/SKILL.md               Character and photo skill
  skills/ettu/references/photos.md   Photo/invitation guidance
```

There are no backend sources, credentials, user records, generated character assets or account-specific tokens in this repository. Users authenticate with their own ettu account. Provider API keys stay on the ettu server.

## What installation includes

This repository contains marketplace catalogs, plugin manifests, the HTTP MCP connection configuration, the ettu and ettu-update skills and their references, release metadata, and installation documentation. There are no install scripts, hooks, local server commands, Python dependencies or bundled credentials. Users authenticate through ettu OAuth; the service runs separately.

Maintainer-only ZIP packaging, validation and release tooling lives in the separate `ettu` application repository. Users do not need that repository or its scripts to install this plugin.
