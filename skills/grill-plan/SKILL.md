---
name: grill-plan
description: Takes a pasted planning/requirements document (기획서, PRD, spec) and automatically runs a grill-me style interview on it, then distills the resolved decisions into a plan document that follows the project's own doc conventions. Use when the user pastes planning/requirements text and wants it stress-tested, or invokes /grill-plan.
---

## Dependencies

| Skill | Type | Install if missing | Source |
|---|---|---|---|
| `grill-me` | optional | `npx skills add mattpocock/skills --skill grill-me -g -a claude-code -y` | https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me |

This skill already describes the grill-me interview rules below, so it works without `grill-me`. If `grill-me` is installed (`~/.claude/skills/grill-me/SKILL.md` or `.claude/skills/grill-me/SKILL.md`), read it and follow its latest rules. If it is missing, you may offer the install command once; install only after the user approves.

<what-to-do>

1. Take the pasted requirements text as the subject — from `$ARGUMENTS` if present, otherwise whatever planning/requirements text the user just pasted. If there is no text at all yet, ask the user to paste it before doing anything else.
2. Read it fully once, then start the grill immediately. Pasting the text into this skill IS the "go" signal — don't ask "should I start?".
3. Interview relentlessly, exactly like `grill-me`: walk every branch of the decision tree, resolve dependencies one by one, one question at a time, always offering your own recommended answer, and wait for the user's response before moving to the next question.
4. If a question is answerable by exploring the codebase (existing patterns, a related feature, naming conventions, a similar prior plan doc) — explore instead of asking.
5. Keep a running decision log as you go (question → resolution → rationale) so nothing gets lost by the end. Don't wait until the end to reconstruct it.
6. When every branch is resolved, or the user says stop/enough, synthesize into a plan document (see below). Don't skip this step silently — confirm the file path with the user before or right after writing it.

</what-to-do>

<supporting-info>

## Where and how to save the plan doc

This skill runs across many different projects — don't assume a fixed layout. Detect the project's own convention each time:

1. Look first for a documented AI-output / docs policy: `CLAUDE.local.md`, `CLAUDE.md`, `CONTRIBUTING.md`, or a `docs/README`/index file — anything that states where planning docs belong, required front-matter, naming pattern, or a registry/index that must be updated when a new doc is added.
2. If found, follow it exactly: tier folder, front-matter fields (e.g. `status` / `updated`), file naming, and register the new doc in whatever index/registry it names. Match an existing registry table's columns exactly — don't invent new ones.
3. If nothing like that exists, default to `docs/plans/<kebab-case-topic>-plan.md` at the repo root, with minimal front-matter:
   ```
   ---
   status: active
   updated: YYYY-MM-DD
   ---
   ```
4. Derive the kebab-case topic from the requirement's subject (the feature/product name), not from the date alone. If a similarly-named plan doc already exists, ask whether to update it in place or create a new variant — don't silently overwrite past work.

## Plan doc structure

Regardless of project, the synthesized doc should contain, in this order:

- **배경/목표** (Background/Goal) — one paragraph: why this exists, what problem it solves
- **확정된 결정사항** (Decisions) — the resolved Q&A log, compressed into statements, not the raw back-and-forth
- **보류/미해결** (Deferred/Open) — anything explicitly deferred, with why
- **범위 밖** (Out of scope) — anything the interview explicitly ruled out, so it isn't re-litigated in a future session
- **다음 단계** (Next steps) — concrete follow-up, e.g. "break down via `/plan` next" or "hand to `/spec`"

## After saving

Report the file path and a short summary of what was decided vs. deferred. Don't paste the full document back into the chat — the file is the source of truth, and the user can open it.

</supporting-info>
