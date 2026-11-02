# Source Discipline Skill (anti-fabrication guardrail)

A Claude skill that makes research and analysis outputs **traceable to sources**. It was written after a real session where a model produced polished-sounding quotes, events and statistics that no source supported.

## What it enforces

| Rule | Effect |
| --- | --- |
| No fabricated quotes | A quote attributed to a named person needs a document the model actually read. Otherwise: "I don't have a sourced quote for that." |
| No fabricated events | Claims that a company launched, acquired, hired or shut down something need a fetched source. |
| **Fetched / Derived / Assumed** | Every number or fact is one of three kinds: read in a source (cite it), computed from fetched numbers (show the arithmetic), or an explicitly labelled assumption. Anything else is not written. |
| Prior output is not a source | A fact repeated across turns is still unsourced unless it was fetched. |
| Search before building | Present-day facts are looked up before they go into a deliverable, not after a challenge. |
| Snippet is not a source | A search snippet only supports what it literally says. |
| Audit the chain | When one error is found, adjacent claims from the same narrative are re-verified. |
| Refuse the polished version | No invented specificity (a precise figure, date or quote) just to match a requested tone. |

## Use

- **Claude Code / Claude skills:** copy `SKILL.md` into a skill folder (for example `~/.claude/skills/non-fabrication/SKILL.md`).
- **Any other assistant:** paste the body of `SKILL.md` at the top of the prompt.

## Why it is written this way

The rules target specific failure modes (fabricated quotes, "plausible business moves", carrying unsourced facts forward) rather than generic "be careful" language. The same design principle runs through my larger projects: [MotoMedic](https://github.com/Maneshwar-Kumar/motomedic-ai) cites every answer to a manual page and fails closed, and [Expert Call Intelligence](https://github.com/Maneshwar-Kumar/expert-call-intelligence) ties every claim to a paragraph anchor.

This is a prompt-level guardrail. It has not been benchmarked, so it reduces the failure modes above but is not a guarantee.
