# Sources

Both sources retrieved and read in full on **2026-09-16** (America/Los_Angeles, PDT).

## 1. Accord — The 2026 Discord Formatting Guide (And Why It Breaks Analysis)

URL: https://www.accord.gg/articles/the-2026-discord-formatting-guide-and-why-it-breaks-analysis
Publisher: Accord (Discord community analysis product), accord.gg
Accessed: 2026-09-16
Type: vendor article / formatting reference + analysis-problem essay
Tags on page: #discord-formatting #discord-markdown #community-analysis #emojis #community-management #discord-tips

Contributes:
- 2026 formatting cheat sheet (bold, italics, underline, strikethrough, bold-italics, inline code, fenced code, spoiler, `>` quote, `>>>` quote, headers H1-H3, `-#` subtext, bullets, numbered, masked link, escape).
- Note that Discord applies markdown client-side → every client renders same chars same way.
- Underscore-inside-word nuance (`snake_case_names` stays readable by design).
- Timestamp format letters and the advice to use `R` in announcements.
- Three emoji kinds (Unicode, custom server, animated) and why emoji are the hardest part for reader and analyst.
- The analysis half: markdown noise, reply chains, threads, chunked messages, language mixing, long messages, junk/short messages.
- How a parser should handle those: markdown-aware tokenisation, reply/thread resolution, message chunking, multilingual classification, context-aware emoji handling, junk filtering without discarding activity.
- Output shape: Topics, Intents (Complaint, Request, Issue, Praise, Question, Thanks, Response), Authors, Cohorts.
- Cohort-level vs message-level reading; the monetization near-miss case study.

## 2. markdownformatting.com — Discord Text Formatting (The Complete Discord Markdown Guide)

URL: https://markdownformatting.com/discord
Publisher: markdownformatting.com
Accessed: 2026-09-16
Type: syntax reference with copy-ready examples and previews

Contributes:
- Full syntax reference with worked examples: bold, italic, bold+italic, strikethrough, mixed emphasis.
- Underline as the Discord-only divergence from standard Markdown (where `__text__` means bold), plus all stacking combos (`__**x**__`, `__*x*__`, `__***x***__`).
- Headers H1-H3, no `####`, space required after the marker.
- Subtext as Discord-exclusive (2024).
- Lists: `-`/`*` bullets, `1.` numbered, 2-space nesting, no checkbox lists.
- Blockquotes: `>`, repeated `>` per line, `>>>` for rest-of-message, no nesting.
- Code blocks: inline vs fenced, language tags, and the fact that code blocks disable all other formatting (includes spoilers).
- Colored text: the ````ansi` block, ESC = U+001B control character (not the literal `\u001b`), format values 0/1/4, text colors 30-37, backgrounds 40-47, combination order (background first), **August 2026 palette swap**, colors now theme-dependent, mobile version dependency, and that color does not travel outside Discord.
- Legacy color trick via highlight.js grammars: ````diff` (red/green), ````fix` (yellow), ````ini` (blue in square brackets), ````bash` (cyan in double quotes).
- Spoilers: inline, multi-line, on files, disabled inside code blocks.
- Links/embeds: masked links (works in normal messages, warning behavior, AutoMod blocking), `<url>` preview suppression, embed field limitations (description/fields full markdown; title/author/footer plain).
- Timestamps: full style table (t, T, d, D, f, F, R) with renders, epoch note, `f` as default.
- Mentions and emoji: `@everyone`, `@here`, `<@id>`, `<@&id>`, `<#id>`, `</command:id>`, `:smile:`, `<:name:id>`, `<a:name:id>`.
- Unsupported list: tables, images, HTML, horizontal rules, task lists, nested quotes, headers past `###`, footnotes/math/Mermaid, font-and-size control — each with a workaround.
- Code-block fake-table workaround for column alignment.
- Escaping section with examples.
- Common mistakes (top 5) with broken→fixed pairs.
- "Where formatting works" surfaces table (desktop, mobile, inside code block, bot/webhook, embed description/fields, embed title/author/footer, channel topic/About Me, usernames+nicknames+thread/forum titles, DMs).
- FAQ covering bold, underline, troubleshooting order, color, tables, masked links, preview suppression, `>` vs `>>>`, `-#`, mobile, timestamps, prevention of formatting, images/HTML.

## Agreement and divergence

- Both sources agree on the core inline set, headers, subtext, lists, quotes, code blocks, spoilers, timestamps, mentions, and escaping.
- Only markdownformatting.com documents ANSI color, the legacy grammar-color tricks, and the surfaces table.
- Only Accord documents the analysis-breaking half (parsing, chunking, emoji-as-signal, cohort reading).
- Accord says masked links are "available in announcements, embeds, webhooks"; markdownformatting.com says they also work in ordinary chat messages (Discord documents them as standard, with a warning when the visible text implies a different destination). This guide uses the broader, more current claim and keeps the caveats.
