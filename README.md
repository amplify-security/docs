# Amplify Security docs

Documentation site for [Amplify Security](https://github.com/amplify-security), built with
[Mintlify](https://mintlify.com/). Configuration lives in `docs.json`.

## Structure

The site has two tabs. **Amplify Console** is the current product, organized into three ideas that build
on each other:

| Group | Covers |
| --- | --- |
| `Get Started` | Introduction, quickstart, CLI installation |
| `Agents & detections` (`agents/`) | The authorable primitives — agents, skills, detections — and the tool surface |
| `Data & connections` (`data/`) | Projects, connections, vendor data, findings |
| `Working interactively` (`interactive/`) | Chat and the CLI |
| `Workflows` (`workflows/`) | Creating, triggering, running, and delivering workflow results |

**Amplify Dashboard (Legacy)** (`legacy/`) documents the previous product and is not actively developed.

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

- Frontmatter requires `title` and `description`.
- Mintlify components in use: `<Note>`, `<Tip>`, `<Warning>`, `<CardGroup>`, `<Card>`.
- Internal links are root-relative and omit the extension — `/agents/writing-an-agent`.
- Document what ships today. Where a capability is partial, say so explicitly in a `<Warning>` or `<Note>`
  rather than describing the intended end state.

## Publishing

The Mintlify GitHub App deploys automatically on push to the default branch.

## Troubleshooting

- **404 on every page** — you're not in the directory containing `docs.json`.
- **A new page isn't in the sidebar** — it isn't registered in `docs.json`.
- **`mint` not found** — install with `npm i -g mint`. Note the CLI is `mint`, not the older `mintlify`
  package, and configuration is `docs.json`, not the older `mint.json`.
