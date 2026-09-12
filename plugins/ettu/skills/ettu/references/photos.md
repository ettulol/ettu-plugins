# Photos and invitations

Use live schemas for exact arguments. The same verified-owner services power the website and MCP.

- Find an owned published character using `get_photo_booth_options(kind: "mine")`. No query shows the main character and three recent others. Search for additional characters.
- For guests, provide the selected owned character and a nonempty query. Search stays within that universe. Never cross universes or infer an invitee’s pose.
- Collect the organizer’s character, background, pose, guest roster and finally optional occasion before `create_photo_booth_photo`. Selfie has no guests; group has 1–5 guests from other creators. Sending invitations requires the user’s instruction. An intentional photo uses a new UUID `request_key`; uncertain delivery preserves the exact arguments and key.
- `get_activity_feed` includes invitations with the selected character and participant state alongside progress and photo results. `list_photo_booth_photos(invitations_only: true)` also reads pending invitations. `get_photo_booth_photo` reads one request and its participant state.
- `respond_photo_booth_invitation` accepts with `accept: true` and the user’s `pose` in the same call. Ask “What pose would you like your character to be doing?” if missing. Declining uses `accept: false` with no pose and cancels the whole group. Everyone must accept. The last acceptance automatically queues one image.
- The organizer may cancel only while invitations are pending. Accepted poses are final. Reactions never accept or decline invitations.
- Completed photos are public. `list_photo_booth_photos` supports public, mine, favorites, album and in_progress scopes, universe filters and pagination. Mine automatically includes character appearances; favorites and album organization are private.
- Use `set_photo_reaction` for happy/love/shocked/sad/scared/laugh, `set_photo_favorite` for favorites, and the album tools for private organization. Album deletion removes only organization.
- Share the returned image/download/page links. Do not claim an external post occurred. Share with Friends uses device sharing when supported, with download and copy-link fallbacks. Reads, delivery retries, reactions, favorites and albums never start a new image generation.

Written poses stay private to their authors; background and occasion stay with the organizer. Never use these fields to deliver messages. Use `mark_activity_read` with the exact id/kind/status to acknowledge a requested notification, and `set_activity_reaction` with its message_id for a requested reaction. Direct messages, personal notes and replies are not supported. A user can create five custom albums plus the built-in Favorites collection.
