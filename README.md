# Amplify Security docs

Documentation site for [Amplify Security](https://github.com/amplify-security), built with
[Mintlify](https://mintlify.com/). Configuration lives in `docs.json`.

## Structure

The site has one tab, **Amplify Console**, organized into three ideas that build on each other:

| Group | Covers |
| --- | --- |
| `Get Started` | Introduction, quickstart, CLI installation |
| `Agents & detections` (`agents/`) | The authorable primitives — agents, skills, detections — and the tool surface |
| `Data & connections` (`data/`) | Projects, connections, vendor data, findings |
| `Integrations` (`integrations/`) | Third-party apps agents can act in — Slack, Atlassian, Linear, Notion, Asana, Google Docs — and how to use their tools in an agent |
| `Working interactively` (`interactive/`) | Chat and the CLI |
| `Workflows` (`workflows/`) | Creating, triggering, running, and delivering workflow results |
| `Reference` (`reference/`, `console/`) | The Console pages map, and the pages of the web console that aren't about agents or workflows — Organization, Billing, Profile |

The previous product, Amplify Dashboard, shuts down on 2026-10-30; its pages were removed and `/legacy/*`
redirects to the introduction.

## Development

Install the Mintlify CLI:

```bash
npm i -g mint
```

Run the dev server from the repository root (the directory containing `docs.json`):

```bash
mint dev
```

It serves on port 3000 by default. Use `--port` if that's taken:

```bash
mint dev --port 3333
```

## Adding a page

1. Create the `.mdx` file in the appropriate directory, with `title` and `description` frontmatter.
2. Register its path (without the `.mdx`) in the correct group in `docs.json`. **A page not listed in
   `docs.json` will not appear in the navigation.**
3. If you move or rename a page, add a `redirects` entry in `docs.json` so existing links keep working.

## Conventions

These pages are also the source the `console-guide` platform skill is generated from (in
`platform-agent-skills`), which is how chat in Amplify Console answers "how do I", "where is", and "can
Console do" questions. The generator reads the pages as written, so the conventions below are a contract
with it, not just house style.

- Frontmatter requires `title` and `description`. The description says what question the page answers —
  *"Where each part of Amplify Console lives and what you do there"* — because it is what the chat sees in
  its index when deciding which page to read.
- Mintlify components allowed: `<Note>`, `<Tip>`, `<Warning>`, `<CardGroup>`, `<Card>` — and only those.
  Any other component needs a change to the `console-guide` generator in `platform-agent-skills` first.
- Name UI elements by their exact label, in bold — **Add connection**, **Save view** — and name the page
  first in any how-to step: *On **Findings**, click **Show filters**.*
- Document what ships today. State an unsupported capability explicitly — "not supported", "not yet" —
  never by omission; a reader (or the chat) can't tell silence from a gap. Where a capability is partial,
  say so in a `<Warning>` or `<Note>` rather than describing the intended end state.
- Internal links are root-relative and omit the extension — `/agents/writing-an-agent`.

## Publishing

The Mintlify GitHub App deploys automatically on push to the default branch.

## Troubleshooting

- **404 on every page** — you're not in the directory containing `docs.json`.
- **A new page isn't in the sidebar** — it isn't registered in `docs.json`.
- **`mint` not found** — install with `npm i -g mint`. Note the CLI is `mint`, not the older `mintlify`
  package, and configuration is `docs.json`, not the older `mint.json`.
