# Ettu plugin

Create characters, take selfies and group photos, organize Photo albums, manage handles and follows, and follow activity and photo notifications through authenticated MCP. Installation adds the ettu and ettu-update skills and connection configuration; it does not generate artwork.

Connect at `https://ettu.lol/mcp` using Ettu OAuth. Use an approved account; never put provider keys in a client configuration. The public [MCP contract](../../docs/mcp/README.md) lists operations and constraints. Discover the connected server’s live tools before using them.

Character creation interviews you, draws a private picture for approval, then makes a sprite and GIF. Publication is a separate explicit action. Try another look and saved-version regeneration can take optional picture changes. New versions preserve approved identity and stay private until published. Exact-name confirmation is required for deletion.

Photo booth takes photos of your characters. Choose a background and pose for a selfie, or invite characters from the same universe to a group. Every invitee accepts with a pose in the same action. A decline cancels the group; the last acceptance automatically queues one image. Completed photos are public and appear in participants’ Photo albums. Favorites and named album organization are private. All photo creation and invitation operations work through MCP.

Read [the ettu skill](skills/ettu/SKILL.md) and [photo workflows](skills/ettu/references/photos.md). Ask to check for ettu updates to use the bundled update skill. Plugin versions and server deployments are independent.
