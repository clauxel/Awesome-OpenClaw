# Contributing to Awesome OpenClaw

**Languages:** **English** | [简体中文](CONTRIBUTING.zh-CN.md)

Thanks for helping keep this list useful.

## Editorial Standard

This repository should be **developer-first, not marketing-first**.

Prefer resources that are:

- official, technical, and durable
- useful during install, configuration, debugging, security hardening, or extension work
- understandable to a normal developer who is evaluating OpenClaw for the first time

Avoid resources that are mostly:

- hype, growth storytelling, or generic news coverage
- fast-staling pricing matrices without clear verification
- unverifiable claims about scale, usage, performance, or popularity
- affiliate-heavy hosting pages that do not actually teach the reader anything

## What Belongs in the README

- Official OpenClaw docs
- Official OpenClaw repositories
- High-signal deployment templates
- Security guides and hardening references
- Skills, plugins, tools, and integrations with concrete developer value
- Deep technical write-ups that explain architecture, deployment, or troubleshooting well

## Multilingual Maintenance

- Treat `README.md` and `CONTRIBUTING.md` as the English source files for structure and intent.
- When you change user-facing guidance, mirror the same change across localized `README.*.md` files and the matching `CONTRIBUTING.*.md` files.
- Keep section order, badges, tables, code blocks, and relative links aligned across languages unless a maintainer asks for a language-specific exception.
- If you can only update one language immediately, note the translation gap in the commit or PR so it can be closed right away.

## How to Add or Update a Resource

1. Edit `README.md`.
2. Mirror the same structural change in each localized `README.*.md` file.
3. Put the link in the smallest relevant section.
4. Add a short description focused on why a developer should click it.
5. Prefer fewer high-value links over larger noisy lists.

### Format

**For bullets:**

```markdown
- [Resource Name](https://link.example) - Short reason this helps developers.
```

**For table rows:**

```markdown
| [Resource Name](https://link.example) | Why it matters |
```

## Writing Rules

- Put official docs before third-party resources.
- Favor action-oriented descriptions over adjectives.
- If a claim is time-sensitive, add a source or date.
- Do not re-introduce giant hosting, pricing, or media lists unless they are carefully verified and genuinely useful.
- Keep the README easy to scan from top to bottom.
- Keep the language switch rows consistent across localized files.
- Treat the maintainer-locked tables in `README.md` as locked unless the maintainer explicitly asks for a change.

## Validation Checklist

Before you add a resource, ask:

- Does this help a normal developer install, run, secure, or extend OpenClaw?
- Is the link still live?
- Is the description specific enough that the reader knows why it matters?
- Would this still be useful in a few months?
- Did you sync the equivalent change across localized files?
- Does the same-language `CONTRIBUTING` link still work from each README?

If the answer is mostly "no", it probably does not belong here.

## Scope

This folder currently maintains markdown documentation, especially `README.md`, localized `README.*.md` files, `CONTRIBUTING.md`, and localized `CONTRIBUTING.*.md` files.

Do not assume website-only files such as `directory.html` or `index.html` exist here unless they are actually added to the repository later.

## Reporting Issues

Please open an issue or send an update when you notice:

- broken links
- outdated setup steps
- incorrect security guidance
- misleading descriptions
- sections that are bloated but not actionable
