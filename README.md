# discord-platform-markdown

Complete Discord markdown master guide for LLMs. Every syntax Discord supports — and every syntax it refuses — plus ANSI color, timestamps, mentions, escaping, which message surfaces actually render markup, and how Discord formatting sabotages downstream analysis if a pipeline reads raw text naively.

## Install

Drop-in Agent Skill. Copy the directory into your agent's skills path:

```bash
git clone https://github.com/gwyntel/discord-platform-markdown-skill.git
cp -r discord-platform-markdown ~/.hermes/skills/discord-platform-markdown
```

Or install from the raw SKILL.md:

```bash
hermes skills install https://raw.githubusercontent.com/gwyntel/discord-platform-markdown-skill/main/SKILL.md
```

## What's inside

- `SKILL.md` — the whole guide, written in compressed "caveman" register so it costs fewer tokens to load while keeping every technical detail exact.
- `references/sources.md` — both sources, what each contributed, where they agree and where they diverge, with accessed date.
- `references/accord-2026-discord-formatting-guide.url` — source 1.
- `references/markdownformatting-discord.url` — source 2.

## Coverage

- Inline: bold, italic, underline (Discord-only divergence), strikethrough, bold-italic, stacking combos, marker-flush rule, mid-word underscore rule.
- Structure: H1–H3, `-#` subtext, bullet/numbered/nested lists, no checkboxes, space-after-marker requirement.
- Quotes: `>`, repeated `>`, `>>>` rest-of-message, no nesting.
- Code: inline vs fenced, language tags, formatting-disabled-inside behavior.
- Spoilers: inline, multi-line, files, dead inside code blocks.
- Links: masked links, preview suppression, embed field limits, no image syntax.
- Mentions and custom emoji ID forms, slash-command links, shortcodes.
- Timestamps: all seven styles incl. relative `R`.
- Color: ```` ```ansi ```` with real U+001B, format/color/background value tables, background-first combination order, the August 2026 palette swap, mobile caveats; plus the legacy ```` ```diff ````/```` ```fix ````/```` ```ini ````/```` ```bash ```` grammar-color tricks.
- Unsupported inventory with workaround for each (tables, images, HTML, rules, task lists, nested quotes, `####`, footnotes/math/Mermaid, font control).
- Escaping and the top five formatting mistakes as broken→fixed pairs.
- Surfaces table: where markdown renders and where it comes out literal (messages, mobile, embeds, channel topic, nicknames, thread titles, DMs).
- Analysis half: markdown noise, reply chains, threads, chunked messages, language mixing, long vs short messages, junk filtering, emoji-as-signal, and the parser design that handles all of it (markdown-aware tokenisation, reply/thread resolution, pre-classification chunking, multilingual classification, context-aware emoji scoring, junk filtering that keeps activity counts). Plus the cohort-vs-message reading lesson.

## Sources

Both read in full on **2026-09-16**.

- Accord — *The 2026 Discord Formatting Guide (And Why It Breaks Analysis)*: <https://www.accord.gg/articles/the-2026-discord-formatting-guide-and-why-it-breaks-analysis>
- markdownformatting.com — *Discord Text Formatting — The Complete Discord Markdown Guide*: <https://markdownformatting.com/discord>

See `references/sources.md` for per-source contribution breakdown.

## Author

gwyntel. Synthesized from the two sources above.

## License

[The Mutualist License v1.2](https://codeberg.org/Mutualism/Mutualist-License) (**MutuaL-1.2**) — strong, network-aware copyleft. If you benefit from this software, you owe the same freedoms to others. Full text in [`LICENSE.md`](LICENSE.md).
