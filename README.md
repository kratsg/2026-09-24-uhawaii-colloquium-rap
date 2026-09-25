# Agents Need Context, Not Just Models

Slides by Giordon Stark (University of Chicago) for the **UH Physics & Astronomy AI
"rap session"** on AI agents for HEP data analysis (24 September 2026). Format per the
session's DJ notes: an informal, open discussion, three slides per speaker (plus an intro), security saved
for the end.

**▶ View the deck:** https://kratsg.github.io/2026-09-24-uhawaii-colloquium-rap/
**▶ Event page:** https://indico.phys.hawaii.edu/event/2985/

The big picture: the model and the harness are swappable; what makes an agent useful (and
safe to trust) is reliable, secure access to the tools, data, and context a facility
already has. The slides are cut down from two earlier talks:

- the Nikhef colloquium, 2026-07-01 ([deck](https://kratsg.github.io/2026-07-01-nikhef-colloquium/#/arch-swap)):
  model / harness / facility-context framing, "ungrounded means silent", agents speak intent
- PyHEP.dev 2026, 2026-09-07 ([repo](https://github.com/kratsg/2026-09-08-pyhepdev-mcp)):
  the AF MCP Platform, MCP server design, and security architecture

The research behind every claim, with commit-level citations, is in
[`mcp-design-talk.md`](mcp-design-talk.md).

## The slides

A title slide plus five short slides (three core slides, one bridge, one MCP intro):

1. **Title** (`#/title`).
2. **"Just furnish context" … from where?** (`#/jfc`): picks up the thread from the JFC
   paper ([arXiv:2603.20179](https://arxiv.org/abs/2603.20179)) and the talks by Kevin Flood
   and Zepeng Li earlier in the session. At a real facility, the context sits behind logins.
3. **Swap the model freely; context makes it useful** (`#/arch-swap`): model, harness,
   facility context and tools, with a "where do my job outputs go?" example.
4. **What is the Model Context Protocol?** (`#/what-is-mcp`): the intro slide from the PyHEP.dev deck.
5. **The MCP Platform: one gateway, many MCP servers** (`#/trace`): the animated
   mcp-portal gateway diagram. Credentials stay behind the broker, every call is authorized,
   and the agent speaks intent.
6. **Secure the architecture, design the interface** (`#/design`): security built into the
   architecture, and "treat the agent like a new student" (clear tasks, a correct manual,
   useful feedback).

## What's here

| Path | What it is |
|------|------------|
| `presentation.html` | The deck (reveal.js 6.0.1, loaded from CDN — no build step) |
| `styles.css` | UChicago-maroon theme (CSS variables, `pt` font sizing) |
| `title-abstract.md` | Title and short description for this session |
| `mcp-design-talk.md` | The full research dossier the slides are built from |
| `images/` | Committed figures |
| `.agents/skills/` | The `revealjs` build skill used to author the deck |
| `.github/workflows/deploy.yml` | Auto-publishes to GitHub Pages on push to `main` |

## View it

- **Online:** the GitHub Pages link above (always reflects `main`).
- **Locally:** open `presentation.html` in a browser. It pulls reveal.js from a CDN, so you
  need a network connection the first time.
- **Speaker notes:** press **`S`** in the browser (allow the popup) for speaker view —
  current + next slide, notes, and a timer. Every slide has notes.
- **Build stamp:** a small footer reads `dev` locally and `<short-sha> · <date>` on the
  deployed site, so you can tell which version is live.

## Edit it

Edit `presentation.html` directly (one slide / a few slides at a time), or use the
in-browser editor from the reveal.js skill:

```bash
node .agents/skills/revealjs/scripts/edit-html.js presentation.html
```

After editing, check for content overflow and review screenshots (Node deps live under
`.agents/skills/revealjs/node_modules`, gitignored — run `npm install` there if missing):

```bash
# flag any slide whose content exceeds 1280×720
node .agents/skills/revealjs/scripts/check-overflow.js presentation.html

# screenshot every slide (export mode disables animations)
.agents/skills/revealjs/node_modules/.bin/decktape reveal "presentation.html?export" \
  output.pdf --screenshots --screenshots-directory "screenshots/$(date +%Y%m%d_%H%M%S)"
```

> Heads-up: media-heavy slides (video / large images) can render *scaled-down* in the
> decktape export — that's a capture artifact. They render correctly in a real browser;
> trust `check-overflow.js` (it reports no overflow) over the decktape thumbnail.

## Deploy

Pushing to `main` triggers `.github/workflows/deploy.yml`, which publishes
`presentation.html` (as `index.html`) + `styles.css` + `images/` to GitHub Pages, injects
the build stamp, and attaches a best-effort `slides.pdf`. One-time setup: repo **Settings →
Pages → Source: GitHub Actions**.

## Credits

Slides AI-assisted by Claude (Anthropic). All quoted code and commit
references are from the real repositories under github.com/maniaclab and github.com/kratsg.
