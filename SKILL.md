---
name: discord-platform-markdown
description: Complete Discord markdown/formatting master guide for LLMs — every syntax Discord supports and rejects, ANSI color, timestamps, mentions, escaping, which surfaces render markup, and how formatting wrecks downstream analysis. Use when writing Discord messages, bot/webhook payloads, embeds, formatting cheats, or parsing Discord message text.
version: 1.0.0
author: gwyntel
license: MutuaL-1.2
compatibility: None — pure knowledge skill, no scripts or network.
metadata:
  hermes:
    tags: [discord, markdown, formatting, messaging, chat-parsing]
    related_skills: [sticker-to-discord-emoji, discord-chat-exporter]
---

# Discord Platform Markdown — Master Guide

Caveman speak. All substance kept. Real syntax exact.

## When to use

- Writing Discord message, bot message, webhook payload, embed.
- Answering "why my formatting no work".
- Writing cheat sheet / formatting hint block for another agent.
- Parsing Discord text: analyst, sentiment, topic, export pipeline.

## Big fact

Discord render markdown **client-side**. Desktop, web, mobile all render same chars same way. Discord use *subset* of Markdown + own additions. Discord does NOT send rendered text — API carries raw markup. Parse raw, resolve markup yourself.

## Inline styles

- `**bold**` → bold. Standard.
- `*italic*` or `_italic_` → italic. Both work.
- `***bold italic***` → bold + italic.
- `__underline__` → underline. **Discord-only.** Standard Markdown say `__x__` = bold. Discord say underline. Disagree here, only here.
- `~~strike~~` → strikethrough.
- `` `inline code` `` → code, short thing: command, filename, status code.
- Stack freely: `***__all four__***`, `__**underline bold**__`, `__*underline italic*__`, `__***all three***__`.

Gotcha: underscore inside word no format. `snake_case_names` stay readable — deliberate, protect code/paths. Want italic mid-word? Use asterisk.

Gotcha: markers must sit flush against first and last char. Space inside = dead. `** bold **` no work.

## Code blocks

- Three backticks fence multi-line. Use for patch notes, logs, crash dumps, any multi-line output.
- Language tag after opening fence (`python`, `js`, `javascript`) → syntax highlighting.
- Code block **switch off all other formatting inside** — bold, spoilers, everything. Good for showing raw symbols. Common reason bold refuses to render.

## Quotes

- `> text` → quote single line. Repeat `>` each line for multi-line.
- `>>>` once → quote everything from there to end of message. Use when replying to long post. No `>` per line needed.
- Discord does **NOT** nest quotes. Extra `>` no stack. Standard Markdown nests — Discord no.

## Headers, subtext, lists

- `# H1` big, `## H2` medium, `### H3` small. Added 2023. One per line, start of line.
- **No `####`** — three levels max.
- `-# text` → subtext: small grey muted. Added 2024. Caption, credit, disclaimer, footnote, "posted on behalf of", timestamp.
- Bullets: `- item` or `* item`.
- Numbered: `1. item`.
- Nest: two spaces before marker.
- Checkbox list NOT supported. `- [ ]` render literal brackets, nothing clickable.

**Hard rule:** every line-start form needs space after symbol — `#`, `##`, `###`, `-#`, `>`, `-`. No space = plain text. Same for `>>>`.

## Spoilers

- `||hidden||` → blacked out till click. Work mid-sentence, across lines, on uploaded files ("Mark as spoiler").
- Spoilers **disabled inside code blocks**.
- Most misused format in gaming servers. Not every hot take = spoiler.

## Links and embeds

- Bare URL auto-links + usually generate preview embed.
- `[text](https://url)` → masked link, hides raw URL. Works in normal chat messages, documented standard feature. Also works in bot embeds, embed descriptions + fields.
- ` <https://url>` → clickable, **suppress preview embed**.
- Caveats masked links: if visible text look like different URL than destination, Discord show confirm warning before open. Server mods can block masked links via AutoMod.
- Embed **title, author, footer** = plain text only. No links, no most formatting.
- `![alt](url)` = nothing. No image syntax. Paste bare image URL (auto-embeds) or upload file.

## Mentions and IDs

- `@everyone`, `@here` — type direct, no ID.
- `<@123456789012345678>` user mention.
- `<@&123456789012345678>` role mention — extra `&`.
- `<#123456789012345678>` channel link → clickable #channel-name.
- `</command:123456789012345678>` slash command link — clicking opens command in message box.
- `:smile:` shortcode → converts to Unicode emoji on send.
- `<:name:123456789012345678>` custom server emoji.
- `<a:name:123456789012345678>` animated custom emoji — leading `a:`.
- Get IDs: Developer Mode on, right-click → Copy ID.

## Timestamps

Not markdown, but most useful formatting Discord has. Unix seconds wrapped in `<t:...>` render in **reader's own timezone and locale**. No math for "9pm my time".

- `<t:1735689600:t>` short time → 4:00 PM
- `<t:1735689600:T>` long time → 4:00:00 PM
- `<t:1735689600:d>` short date → 01/01/2025
- `<t:1735689600:D>` long date → January 1, 2025
- `<t:1735689600:f>` short date+time (DEFAULT when style omitted) → January 1, 2025 4:00 PM
- `<t:1735689600:F>` long date+time → Wednesday, January 1, 2025 4:00 PM
- `<t:1735689600:R>` relative, self-updating → "in 2 hours" / "2 months ago"

Use `R` in announcements: "patch drops in 4 hours" stays true across every timezone.

## Color — ansi code block

Discord have NO color syntax for ordinary messages. No way to color word mid-sentence. Only path = ```` ```ansi ```` code block with real ANSI escape sequences.

Form: open ```` ```ansi ````, prefix each run with `ESC[format;color m`, close with `ESC[0m`.

- `ESC` = **invisible control char U+001B**, NOT the 8 characters `\u001b`. Typing `\u001b` does nothing. Must copy real char (tool generator, or produce programmatically).
- Values combine in one prefix, **background first**: `ESC[1;40;32m` = bold green on black. `ESC[1;4;31m` = bold underlined red.
- Palette swapped **August 2026** — backgrounds 40-47 changed entirely, colors now shift with reader's theme.
- Desktop + browser always render color. Mobile: recent app versions render; older installs show plain monospace. Treat as enhancement.
- Color does NOT travel. Paste anywhere but Discord = plain code block.

Format values: `0` normal, `1` bold, `4` underline.
Text colors 30-37: 30 black, 31 red, 32 green, 33 brown, 34 light blue, 35 pink, 36 teal, 37 light gray.
Background 40-47: 40 black, 41 red, 42 green, 43 brown, 44 light blue, 45 pink, 46 teal, 47 light gray.

### Old color trick — syntax highlighting

Before ANSI, color came from picking language whose highlight.js grammar paints whole line. Cruder: one color per line, only colors grammar makes. But no invisible chars, survives old mobile.

- ```` ```diff ```` → lines starting `-` red, `+` green.
- ```` ```fix ```` → everything yellow.
- ```` ```ini ```` → text in `[square brackets]` blue.
- ```` ```bash ```` → text in `"double quotes"` cyan.

## Not supported — do not try

- **Tables** — no pipe tables. Raw text garbage. Workaround: line up columns with spaces inside plain code block (monospace keeps alignment), or post screenshot.
- **Images** — `![alt](url)` dead. Bare URL or upload.
- **HTML** — no tags. `<b>`, `<br>`, `<span style>` render literal.
- **Horizontal rules** — `---` and `***` plain text. No divider syntax.
- **Task lists** — `- [ ]` / `- [x]` literal brackets, not clickable.
- **Nested quotes** — extra `>` no stack; `>>>` not "level three", it eats rest of message.
- **Headers past `###`** — `####` + deeper not headings.
- **Footnotes, math, Mermaid** — none.
- **Font/size control** — headers + subtext only size options. No color or font syntax outside ansi block.

## Escaping

Backslash `\` before formatting char = send literal.

- `\*\*not bold\*\*` → **not bold**
- `\|\|not a spoiler\|\|` → ||not a spoiler||
- `` \`not code\` `` → `not code`
- `\> not a quote` → > not a quote
- `\` before custom emoji → reveals `<:name:id>` form.

Whole message escape: wrap in code block. Kills every other format.

## Common mistakes — top 5

1. Space inside markers: `** bold **` dead → `**bold**`.
2. No space after `#` / `-##` / `>` / `-`: `#Header` plain text → `# Header`.
3. `__text__` = underline on Discord, not bold. Use `**` for bold everywhere.
4. `**bold**` inside code block → dead. Formatting not active inside code.
5. `\u001b` typed literally in ansi block → nothing. Need real U+001B char.

## Where formatting works

- Desktop/browser messages: FULL, ansi included.
- Mobile app messages: all text formatting. ANSI on recent versions only.
- Inside code block: NO — all formatting off by design, spoilers too.
- Bot + webhook messages: YES, same syntax as user message, plus rich embeds via API.
- Embed description + fields: FULL markdown, masked links included.
- Embed title, author, footer: PARTIAL — plain text only.
- Channel topic + About Me: PARTIAL — inline formatting + links render, headers and lists generally not.
- Usernames, nicknames, thread titles, forum titles: NO — plain text fields, chars show literal.
- Direct messages: YES, identical to server channel.

Rule: Discord renders markdown in **message content**. Many other text fields do not. Second-most-common reason syntax comes out literal.

## Quick ref — every syntax

- Bold `**text**` — standard
- Italic `*text*` / `_text_` — standard
- Bold+italic `***text***` — standard
- Underline `__text__` — Discord-only
- Strikethrough `~~text~~` — standard
- Header 1-3 `# / ## / ### text` — Discord-only (2023)
- Subtext `-# text` — Discord-only (2024)
- Inline code `` `code` `` — standard
- Code block ``` ```code``` ``` — standard
- Colored text ```` ```ansi ```` + `ESC[1;32m` — Discord-only, needs recent app on mobile
- Blockquote `> text` — standard
- Rest-of-message quote `>>> text` — Discord-only
- Spoiler `||text||` — Discord-only
- Bullet `- item` — standard
- Numbered `1. item` — standard
- Masked link `[text](url)` — standard
- Suppress preview `<url>` — Discord-only
- Timestamp `<t:1735689600:R>` — Discord-only
- User/role/channel mention `<@id>` / `<@&id>` / `<#id>` — Discord-only
- Custom emoji `<:name:id>` — Discord-only
- Escape `\* \_ \~` — standard

## Other half — formatting breaks analysis

Formatting = few strokes to reader. To machine reading server *after the fact*, same chars = wall of noise. Real problems for any pipeline:

- **Markdown noise.** Raw text full of `**`, `~~`, `||`, backticks. Read `**bug**` as different token than `bug` → sentiment + topic models fall apart. Blind strip: player's pasted crash log inside code block becomes indistinguishable from narrative complaint.
- **Reply chains.** "yeah this" meaningless alone, decisive in context. Unresolved `replied to` link = half the agreement signal gone.
- **Threads.** Thread = own scoped conversation off parent channel. Read main channel only = miss the deep-dive discussions product teams want most.
- **Chunked messages.** Players no write paragraphs. "so this happened" / "and then the patch dropped" / "and now damage scaling broken on mage" — three messages in twelve seconds, one thought. Classify independently = three topics instead of one complaint.
- **Language mixing.** Big communities thread English, German, Russian, Spanish, Korean in one channel. Single-language tooling misses everything non-English.
- **Long messages.** 3,000-word economy manifesto ≠ 3,000 two-word messages. Both signal. Not same signal.
- **Junk + short messages.** `gg`, `+1`, 👀, `/join`. Real engagement, zero analytical content alone. Must count as activity without polluting topic analysis.

Any one solvable alone. All at once, tens of thousands to millions messages/month, at live-service speed = the actual problem.

### How to parse formatted Discord proper

- **Markdown-aware tokenisation.** Parse formatting, not strip. Word inside `**bold**` stays same token as plain word. Emphasis becomes a feature, not garbage input.
- **Reply + thread resolution.** Every message knows parent, thread, channel. "yeah this" scored against message it answers. Threads analysed as own scoped context.
- **Message chunking.** Group close-together messages from same author on same subject into one conversational unit *before* classification. Three-message thought lands as one topic.
- **Multilingual classification.** Handle languages community actually uses. No forced single locale default.
- **Context-aware emoji handling.** Score emoji as sentiment + intent modifiers, do not strip. `🙃` flips sentiment of sentence it lands in. `💀` in bug report ≠ `💀` in joke reply.
- **Junk filtering without discarding activity.** Short acknowledgements + single emoji move activity metrics; must not confuse topic counts.

Output shape: structured **Topics**, **Intents** (Complaint, Request, Issue, Praise, Question, Thanks, Response), **Authors**, **Cohorts** — queryable.

### Emoji — three kinds, all carrying meaning

- **Unicode** — 🔥 👀 💀. Meaning from culture: 💀 almost never about death, 🔥 almost never about fire.
- **Custom server** — `:pepepoggers:`, `:serverlogo:`. Meaning specific to server, changes over time.
- **Animated** — same as custom with motion. Nitro users drop anywhere.

Emoji hardest part of formatting for reader AND analyst. `"great new balance update 🙃"` is not a compliment. Thumbs-up on bug report = "acknowledged", "me too", or "closed-won't-fix" — ambiguous. Symbol does work words don't, in ways that don't generalise across communities, games, even channels.

**Rule for pipelines: never strip emoji. Never treat as noise.** Stripping loses the most important half of the signal.

### Vote-count illusion

Real case: team almost shipped monetization change based on one vocal new user. Cohort analysis showed veterans + other new users explicitly saying current model fine. Read at **cohort level**, not message level.

## Sources

Both fetched and read in full **2026-09-16**. See `references/sources.md`, plus one `.url` per source in `references/`.

- Accord — "The 2026 Discord Formatting Guide (And Why It Breaks Analysis)": `https://www.accord.gg/articles/the-2026-discord-formatting-guide-and-why-it-breaks-analysis` — formatting cheat sheet half + the analysis/parsing half (markdown noise, reply chains, threads, chunking, multilingual, emoji, junk filtering, cohort reading).
- markdownformatting.com — "Discord Text Formatting — The Complete Discord Markdown Guide": `https://markdownformatting.com/discord` — exhaustive syntax: text styles, underline stacking, headers, subtext, lists, blockquotes, code blocks, ANSI color + palette, legacy highlight-color tricks, spoilers, links/embeds, timestamps, mentions/emoji, unsupported list, escaping, mistakes, surfaces table, FAQ.

Both agree on core set. Difference worth noting: markdownformatting.com documents ANSI color + legacy color tricks + surfaces table; Accord documents the analysis-breaking half. This guide = both, combined, no duplication.
