# BrewBot feature documentation audit

Reviewed October 4, 2026 against local `brew-bot` commit `08656cf3` (`feat: add selectable Rate Me screen time`). This is a source audit of the dashboard, relevant validation/access routes, bot handlers, and the bundled Stream Deck plugin; it is not a claim that every feature was exercised against production accounts. The app repository was not changed.

## Coverage

Every entry in `src/components/manage-navigation/config.ts` is mapped below, including section landing pages. Route suffixes are relative to `/manage/[serverId]`; feature pages and their component directories live under `src/app/manage/[serverId]`. Read API and runtime checks as well as navigation labels: some labels lag behind behavior.

| Dashboard entry | Route suffix | Documentation |
| --- | --- | --- |
| Dashboard | `/` | [index](index.mdx) |
| Server Management | `/server-management` | [getting-started/onboarding](getting-started/onboarding.mdx) |
| Channel Manager | `/channels` | [features/channel-role-manager](features/channel-role-manager.mdx) |
| Role Manager | `/roles` | [features/channel-role-manager](features/channel-role-manager.mdx) |
| Reaction Roles | `/reaction-roles` | [features/reaction-roles](features/reaction-roles.mdx) |
| Reports | `/reports` | [features/reports](features/reports.mdx) |
| Custom Commands | `/custom-commands` | [features/custom-commands](features/custom-commands.mdx) |
| Welcome Message | `/welcome-message` | [features/welcome-messages](features/welcome-messages.mdx) |
| Birthdays | `/birthdays` | [features/birthdays](features/birthdays.mdx) |
| Moderation | `/moderation` | [getting-started/onboarding](getting-started/onboarding.mdx) |
| Mod Logs | `/mod-logs` | [features/mod-logs](features/mod-logs.mdx) |
| Mod Agreements | `/mod-agreements` | [features/mod-agreements](features/mod-agreements.mdx) |
| AutoMod | `/automod` | [features/automod](features/automod.mdx) |
| Captcha Verification | `/captcha-verification` | [features/captcha-verification](features/captcha-verification.mdx) |
| Engagement | `/engagement` | [getting-started/onboarding](getting-started/onboarding.mdx) |
| TikTok Alerts | `/alerts` | [features/social-alerts](features/social-alerts.mdx) |
| Twitch Alerts | `/twitch-alerts` | [features/social-alerts](features/social-alerts.mdx) |
| Kick Alerts | `/kick-alerts` | [features/social-alerts](features/social-alerts.mdx) |
| OnlyFans Alerts | `/onlyfans-alerts` | [features/social-alerts](features/social-alerts.mdx) |
| YouTube Alerts | `/youtube-alerts` | [features/social-alerts](features/social-alerts.mdx) |
| Leveling | `/leveling` | [features/leveling](features/leveling.mdx) |
| Polls | `/polls` | [features/polls](features/polls.mdx) |
| Brewlinks | `/brewlinks` | [features/brewlinks](features/brewlinks.mdx) |
| BrewBot Messages | `/messages` | [features/messages](features/messages.mdx) |
| Agent Connections | `/agent-connections` | [integrations/agent-connections](integrations/agent-connections.mdx) |
| Live Tools | `/live-tools` | [features/live-tools](features/live-tools.mdx) |
| TikTok Rankings | `/live-tools/rankings` | [features/tiktok-rankings](features/tiktok-rankings.mdx) |
| TikTok Chat Monitor | `/live-monitor` | [features/live-monitor](features/live-monitor.mdx) |
| Twitch Monitor | `/twitch-monitor` | [features/twitch-monitor](features/twitch-monitor.mdx) |
| Transcripts | `/transcripts` | [features/transcripts](features/transcripts.mdx) |
| Schedule | `/live-tools/schedule` | [features/schedule](features/schedule.mdx) |
| Speed Tracker | `/live-tools/speed-tracker` | [features/speed-tracker](features/speed-tracker.mdx) |
| Dare Grid | `/live-tools/dare-grid` | [features/dare-grid](features/dare-grid.mdx) |
| Profiles | `/live-tools/speed-tracker/profiles` | [features/speed-tracker](features/speed-tracker.mdx) |
| Tickets | `/live-tools/speed-tracker/tickets` | [features/tickets](features/tickets.mdx) |
| Blocked From Live | `/live-tools/live-blocks` | [features/live-blocks](features/live-blocks.mdx) |
| Gift Goals | `/live-tools/gift-goals` | [features/gift-goals](features/gift-goals.mdx) |
| Rate Me | `/live-tools/rate-me` | [features/rate-me](features/rate-me.mdx) |
| Game Requests | `/live-tools/game-requests` | [features/game-requests](features/game-requests.mdx) |
| Gift Sounds | `/live-tools/gift-sounds` | [features/gift-sounds](features/gift-sounds.mdx) |
| Timer Gifts | `/live-tools/timer-gifts` | [features/timer-gifts](features/timer-gifts.mdx) |
| Overlays | `/live-tools/overlays` | [features/overlays](features/overlays.mdx) |
| TTS Settings | `/live-tools/tts-settings` | [features/tts](features/tts.mdx) |
| Live Commands | `/live-tools/live-commands` | [features/live-commands](features/live-commands.mdx) |
| TTS Story | `/live-tools/tts-story` | [features/tts-story](features/tts-story.mdx) |
| Spotify | `/live-tools/spotify` | [integrations/spotify](integrations/spotify.mdx) |
| Apple Music | `/live-tools/apple-music` | [integrations/apple-music](integrations/apple-music.mdx) |
| Configuration | `/configuration` | [getting-started/onboarding](getting-started/onboarding.mdx) |
| Bot Settings | `/bot-personalizer` | [features/bot-personalizer](features/bot-personalizer.mdx) |
| Integrations | `/integrations` | [integrations/platform-connections](integrations/platform-connections.mdx) |
| Billing | `/billing` | [getting-started/billing](getting-started/billing.mdx) |
| Permissions | `/permissions` | [features/permissions](features/permissions.mdx) |
| API Logs | `/api-logs` | [integrations/api-logs](integrations/api-logs.mdx) |

Additional surfaces reviewed:

| Surface | Documentation | Primary source |
| --- | --- | --- |
| Account onboarding and installation | Getting started | `src/app/manage/onboarding`, `src/app/manage/install` |
| Team membership and server administration | Teams | `src/app/manage/teams`, `src/lib/server-access-policy.ts`, `src/lib/auth-helpers.ts` |
| Custom bot setup and voice/AI settings | Custom bot; Bot Settings | `bot-personalizer/components`, `api/servers/[serverId]/custom-bot`, `subscription-shared.ts` |
| TikTok and Twitch audio players | TikTok TTS; Twitch TTS | `src/app/player`, `src/components/tts-player/TtsBrowserPlayer.tsx` |
| Public overlay routes | Stream overlays and each feature | `src/app/overlay` |
| Public ticket/status/registry forms | Tickets | `src/app/speed-tracker/tickets`, `src/app/api/public/speed-dating-tickets` |
| Public contact status | BrewBot Messages | `src/app/message/page.tsx` |
| Slack install, overview, assistant, summaries, alerts, settings, billing | Slack workspaces | `src/app/manage/slack`, `src/lib/slack-workspaces.ts`, `slack/src` |
| Discord slash and prefix commands | Bot commands; Custom commands; Leveling | `bot/src/commands`, `bot/src/lib/commands.ts`, `bot/src/events/customCommands.ts` |
| Cursor and Brave tools | Agent Connections; Cursor Cloud Agents | `src/app/manage/[serverId]/agent-connections`, `src/lib/agent-tools` |
| Bundled Stream Deck actions and requirements | Stream Deck | `public/downloads/BrewBot.streamDeckPlugin` manifest and property inspector |

## Important behavior verified

- Sound uploads: `src/lib/gift-sound-upload-policy.ts`, `gift-sound-validation.ts`, `gift-sound-uploads.ts`, upload routes, `CustomSounds.tsx`, and `bot/src/lib/giftSounds.ts`. MP3/PCM WAV, 5 MB, 30 seconds, 50 per server, five-second pacing; deletion clears assignments. Playback shares the TikTok TTS queue and supports repeated gifts.
- Timer Gifts: settings page, `api/servers/[serverId]/timer-gifts/settings`, `bot/src/lib/speedDatingTimerGift.ts`. Gifts extend a running timer by three minutes once per countdown; they cannot start it, despite the older navigation description.
- Rate Me: `src/lib/rate-me.ts`, settings route, and page. Screen time is 5–30 seconds in five-second steps, default 30; one-minute cooldown, 25-viewer queue.
- TTS: `bot/src/lib/speedDatingChatTts.ts`, `bot/src/lib/twitchChatTts.ts`, `src/lib/speed-dating-chat-tts.ts`, settings components, and browser player. Both platforms gate new requests during the running timer. Twitch whitelist is additive, not a whitelist-only mode. TikTok includes active Heart Me access, MVPs, voice overrides, stories, and shared gift audio.
- Billing: `src/lib/billing-pricing.ts`, `subscription-shared.ts`, `subscription.ts`, `stripe.ts`, checkout and custom-bot routes. Standard price is $25 monthly / $249 annual; five-day trial; current checkout contains no mandatory $149 setup item. Birthdays and basic/custom bot setup are free; mod agreements and AI settings are premium. Actual customer arrangements remain authoritative on Billing.
- Commands: birthday input is `date`, XP target is `user`, `/rank` accepts a target, `/ticket` returns a form URL, `/image` accepts an attachment, `/level-test` is diagnostic, and `/bot-health` requires Manage Server.
- Reports publishes a Discord ticket-form panel. Transcripts record TikTok LIVE events and expire 24 hours after creation. Mod Agreements records acknowledgments rather than granting roles.
- Custom Commands: current UI is a prefix-message editor. Role actions are marked `available: false`; there is no selectable slash-command type. The API allows up to 500 commands per server.
- Poll recurrence: `bot/src/events/polls.ts` creates the next scheduled occurrence on successful posting. Cancel the next unposted occurrence to stop the chain; ending the active poll does not cancel the next one.
- Team access: per-member server selection and per-server admin assignments are distinct from Team Admin. Speed Dating/profile deletion can follow server-admin authority; Dare Grid still requires its own permission.
- Apple Music: playback runs in a regular browser audio controller; OBS is display-only. Some old UI copy still calls the OBS source the playback controller.
- Social alerts include Kick and OnlyFans. The current YouTube flow tracks LIVE streams rather than generic uploads.

## Limits and follow-up items

- Slack summary/digest and alert controls persist settings, but no scheduled digest worker or automatic alert-forwarding consumer was found in the reviewed runtime. The Slack guide states this limit; it does not advertise confirmed delivery.
- Screenshots are not available from authenticated app sessions. Published guides retain/add screenshot TODOs as required by `AGENTS.md`.
- Gift Sounds navigation requires Speed Dating access, while upload/settings APIs check server access and premium `speedTracker` entitlement. The guide distinguishes the navigation restriction rather than claiming an extra API restriction.
- Timer style availability can vary by server. The guide tells readers to choose an available style instead of promising every themed style globally.
- The registry form is server-specific. It is described as an optional team-provided link, without advertising it as globally enabled.
- Super-admin pages, internal QA tooling, profile transfers in admin, and operational infrastructure are excluded from public docs. Portfolio, legal, and sign-in pages are not bot feature guides. Redirect/section landing routes point to the corresponding setup or feature overview.
- Budget alerts, rank-card customization, welcome embeds, role actions in the command editor, and streaming auto-role cards marked unavailable/coming soon are not documented as working features.

## Validation

Run `npx mint validate`, `npx mint broken-links`, and `git diff --check` after edits. Also verify that every navigation page exists, every publishable MDX page is in navigation, imports resolve, and root-relative links and heading anchors resolve. Keep this file excluded by `.mintignore`.

Final checks on October 4, 2026:

- Mintlify build validation passed.
- Mintlify broken-link check passed.
- All 52 publishable MDX pages appear exactly once in navigation.
- All 144 internal links, including heading anchors, resolve; frontmatter and snippet imports were checked.
- All 53 dashboard navigation entries are mapped above.
- `git diff --check` passed.
