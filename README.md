# Claude Code — Professional Guide to Optimizing Tokens, Context, and Resources

> **Practical handbook | October 15, 2026 edition | Language: English**  
> Focus: software development with Claude Opus models (including the model referred to by the user as “Opus 5.5”), Claude Code on Windows, and WordPress, TypeScript, Node.js, and Electron projects.

---

## Table of Contents

1. [Goals and core principles](#1-goals-and-core-principles)
2. [Quick start: 12 golden rules](#2-quick-start-12-golden-rules)
3. [Initial configuration and model selection](#3-initial-configuration-and-model-selection)
4. [Reasoning effort](#4-reasoning-effort)
5. [Context, clear, compact, and work continuity](#5-context-clear-compact-and-work-continuity)
6. [Prompt caching: preserving its benefits](#6-prompt-caching-preserving-its-benefits)
7. [Exploring repositories with minimal overhead](#7-exploring-repositories-with-minimal-overhead)
8. [CLAUDE.md, project rules, and skills](#8-claudemd-project-rules-and-skills)
9. [Subagents and cheaper models: when they pay off](#9-subagents-and-cheaper-models-when-they-pay-off)
10. [MCP, LSP, hooks, and automation](#10-mcp-lsp-hooks-and-automation)
11. [Testing, debugging, and preventing loops](#11-testing-debugging-and-preventing-loops)
12. [Everyday Claude Code commands](#12-everyday-claude-code-commands)
13. [Ready-to-copy prompts](#13-ready-to-copy-prompts)
14. [Realistic scenarios: WordPress, Electron, TypeScript](#14-realistic-scenarios-wordpress-electron-typescript)
15. [A complete professional daily workflow](#15-a-complete-professional-daily-workflow)
16. [Measuring results, quotas, and savings](#16-measuring-results-quotas-and-savings)
17. [What NOT to do: false optimizations](#17-what-not-to-do-false-optimizations)
18. [Operational checklists](#18-operational-checklists)
19. [Ready-to-use CLAUDE.md template](#19-ready-to-use-claudemd-template)
20. [Glossary and official sources](#20-glossary-and-official-sources)

---

## 1. Goals and core principles

The goal is **NOT** to make Claude produce code faster by skipping important verification steps. The goal is to **achieve the best technically correct result while minimizing unnecessary model work**.

Three separate metrics matter:

| Metric | What it measures | Why it matters |
|---|---|---|
| **Tokens processed** | Input, output, reasoning, and context associated with requests | Indicates how much work the system performs |
| **API cost** | Amount billed according to the model, caching, provider, and rates | Matters when paying per API request |
| **Plan usage limits** | How much capacity remains in your subscription | Matters for Claude Pro/Max or other plans |

**Important:** halving one type of token does not necessarily halve your plan usage. Caching, model choice, request characteristics, and provider policies all affect the outcome.

Guiding principle: **search → read narrowly → decide → change narrowly → test selectively → summarize**.

## 2. Quick start: 12 golden rules

1. **Define one specific task** before asking Claude to explore an entire project.
2. **Match `/effort` to task complexity:** lower for simple tasks, higher only for genuinely difficult problems.
3. **Check `/context`** before a long session becomes unwieldy.
4. **Use `/clear` when switching tasks**, and `/compact` when continuing the same work but needing context space.
5. **Do not ask Claude to “read the entire project”** without a good reason: search for symbols, filenames, and references.
6. **Filter logs** before bringing them into the conversation.
7. **Run the most relevant tests first**, then widen coverage where necessary.
8. **Keep `CLAUDE.md` short and useful**, not a complete manual.
9. **Load specialized skills on demand** instead of keeping lengthy instructions always active.
10. **Use only the MCP servers and parallel agents you need.**
11. **Stop unproductive loops** and request a fresh diagnosis.
12. **Measure with `/usage` and `/insights`** instead of trusting theoretical savings percentages.

## 3. Initial configuration and model selection

### Initial checks

From the terminal in your project directory:

```powershell
claude --version
claude
```

Inside Claude Code:

```text
/model
/effort
/usage
/context
/mcp
```

**Compatibility:** commercial model names and available effort levels change over time. If you are using a model called “Opus 5.5,” check the actual model identifier through `/model`. This guide does not assume that every option is available in every release or account.

### Recommended profile

| Task type | Preference | Notes |
|---|---|---|
| Critical architectural decisions | Opus; higher effort if necessary | Requires analysis and verification |
| Routine implementation | Suitable model, medium effort | Avoid overpowered setups for simple work |
| Renaming, formatting, small changes | Low effort or deterministic tools | Validate automatically |
| Repetitive log analysis | CLI/script or cheaper subagent | Return a compact result |
| Sensitive security review | Strong model plus independent checks | Never sacrifice security |

Do not switch models for every message: coordination overhead and lost continuity can outweigh the benefits.

## 4. Reasoning effort

Claude Code documents the following command family:

```text
/effort
/effort low
/effort medium
/effort high
/effort xhigh
/effort max
/effort auto
```

The levels you can actually select **depend on the model and release**. `max` is only available in supported contexts and may be session-scoped.

| Level | Use for | Avoid for |
|---|---|---|
| `low` | Trivial edits, UI text, known files, narrowly scoped fixes | Data migrations, security, complex bugs |
| `medium` | Normal features, iterative development, maintenance | Extremely difficult unresolved problems |
| `high` | Difficult debugging, concurrency, risky integrations | Simple renames and CSS tweaks |
| `xhigh` / `max` | Only when supported and the problem genuinely warrants exceptional depth | Your global default |

**Practical rule:** start at `medium` for a normal feature; increase it only when meaningful ambiguity or complexity appears. There is no universal savings percentage.

**Note:** do not rely on legacy variables such as `MAX_THINKING_TOKENS` to control adaptive reasoning in newer models. Always check the documentation for your installed version.

## 5. Context, clear, compact, and work continuity

Conversation history can become the main source of inefficiency: searches, tool outputs, and unsuccessful attempts may remain part of subsequent requests.

| Command | Effect | Recommended use |
|---|---|---|
| `/context` | Shows how the context window is being used | Periodically, or when sessions become cumbersome |
| `/compact` | Summarizes work to free context space | Same task, long-running session |
| `/compact <instructions>` | Specifies what the summary should preserve | Before another demanding phase |
| `/clear` | Starts a fresh conversation without prior history | Clear task switch |
| `/resume` | Resumes a previous session | Interrupted work |
| `/btw <question>` | Side question without adding to the main history | Occasional clarification |
| `/rewind` | Returns to a checkpoint, subject to supported options | When work has gone in the wrong direction |

### Example: compact effectively

```text
/compact Preserve the current goal, architectural decisions, modified files,
test commands and results, outstanding errors, and exact next steps.
Discard outdated searches, verbose logs, and disproven hypotheses.
```

### When to use `/clear`

- You have finished authentication and are moving on to an unrelated dashboard.
- Your session contains dozens of now-irrelevant outputs.
- You want an independent review without inheriting previous assumptions.

### Mini handoff before a new session

Optionally create a `WORKLOG.md` file:

```markdown
# Handoff
- Goal: fix settings persistence
- Status: reproduced; cause isolated to settings module
- Modified files: src/settings/store.ts
- Passing tests: store unit tests
- Missing tests: UI integration
- Next action: fix debounce and test on Windows
- Constraints: do not change public APIs
```

**Avoid excessive compaction:** generating summaries takes work and may disrupt caching benefits. Do not compact every five messages out of habit.

## 6. Prompt caching: preserving its benefits

Prompt caching can reduce the cost of reprocessing repeated inputs. It does not mean that context tokens cease to exist.

Good practices:

- Keep **global instructions stable** across related tasks.
- Avoid repeatedly adding and removing MCP servers and tools in the middle of a session.
- Avoid constantly changing rule files that are reread on subsequent requests.
- Do not use `/clear` for a quick question if the current context is still valuable.
- Review caching information in `/usage`, **when supported by your version and provider**.

### Understanding `/usage`

Conceptual example:

```text
Input tokens: ...
Output tokens: ...
Cache read: ...
Cache write: ...
```

- **High cache reads:** substantial input was served from cache.
- **High cache writes:** substantial material was prepared for reuse.
- **Cache misses:** some content had to be processed again.

Do not maximize cache hits at any cost: an enormous conversation may still become difficult to work with, even if part of it is cached.

## 7. Exploring repositories with minimal overhead

### Inefficient pattern

> Read the entire repository, inspect every file, then find out why login freezes.

### Better pattern

> First locate the files implementing login, sessions, and tokens. Search by filenames and symbols; read only relevant sections, develop a diagnosis, and change only what is necessary. Do not dump complete logs.

### Practical Windows PowerShell commands

**Find relevant files:**

```powershell
rg --files src | rg 'auth|login|session|token'
```

**Find symbols without reading whole files:**

```powershell
rg -n 'authenticate|refreshToken|createSession' src
```

**Display only a file excerpt:**

```powershell
$lines = Get-Content 'src/auth/session.ts'
$lines | Select-Object -Skip 79 -First 80
```

**Filter compiler errors:**

```powershell
npx tsc --noEmit --pretty false 2>&1 | Select-String 'error TS'
```

**Run a targeted test (if project scripts support it):**

```powershell
pnpm test -- auth
```

> `rg` requires ripgrep, and `pnpm` must be installed. Inspect your project scripts before running commands. Filtering logs can hide important details: expand the output when the initial diagnosis is insufficient.

### Useful exclusions

You generally do not need to read large amounts of `node_modules/`, `dist/`, `build/`, `.next/`, `coverage/`, `.git/`, old logs, or generated files. Do not exclude a file that is directly relevant to the issue.

## 8. CLAUDE.md, project rules, and skills

`CLAUDE.md` contains recurring instructions. Because it is commonly loaded into sessions, redundant text can create persistent overhead.

**Good practice:** keep it concise (roughly 200 lines or fewer as a working guideline) and include non-obvious information Claude needs for your project.

Include in `CLAUDE.md`:

- Essential stack information and conventions.
- Reliable build/test commands.
- Architectural boundaries and sensitive files.
- Minimum quality standards.
- Preferences for exploration and responses.

Do not include:

- Long TypeScript or WordPress tutorials.
- Full copies of official documentation.
- Lengthy descriptions of every file.
- Large logs or chat histories.

Create on-demand skills for specialized topics such as `release`, `wordpress-security-review`, `electron-packaging`, and `database-migrations`.

### Example

**In CLAUDE.md:** “For Windows releases, use the dedicated release skill.”

**In the skill:** signing procedures, packaging tests, updates, and publishing.

This avoids loading release instructions during a simple UI bugfix.

## 9. Subagents and cheaper models: when they pay off

A subagent has a **separate context** and can return only its findings to the main agent. This helps isolate noise; it does not automatically reduce total token usage.

### Effective example

**Main agent (Opus):** determines how to address a bug.

**Exploration subagent (cheaper model when configurable):** searches for every call to `saveSettings` and returns a file list and five findings without copying the entire source.

**Main agent:** receives a short summary and implements the fix.

### When NOT to delegate

- Changing one interface string.
- Renaming a local variable.
- Running a single test command.
- Working on an already identified single file.

### Decision rule

Delegate only when the **context saved and/or useful parallel execution** justify the additional agent overhead. Agent teams running many simultaneous instances can substantially increase total consumption.

## 10. MCP, LSP, hooks, and automation

### MCP

MCP integrations connect external tools and services. Each server adds capabilities but may also add context and tool-call overhead.

Check:

```text
/mcp
/context
```

Keep only the MCP servers actually needed for the current project. If you just need Git history, a local `git log` command may be simpler than a remote tool call.

### LSP / code intelligence

Code-intelligence integrations can locate definitions, references, and type errors more precisely than bulk reading. They require an appropriate integration or plugin for the language.

### Deterministic hooks

Prefer a script or hook for mechanical, repeatable jobs:

- Format files after edits.
- Lint changed files.
- Prevent edits to protected files.
- Trim excessively verbose command output.

**Illustrative logic (pseudocode, NOT a complete hook configuration):**

```text
After a file is modified:
  if extension == .ts:
    run local formatter
    run targeted lint
    return only status and the first useful errors
```

Hooks need testing: poorly designed automation can create repeated work or conceal errors.

### Scheduled tasks and loops

Every execution may trigger model requests, tool calls, and token usage. Schedule work only when useful, and inspect consumption with `/usage`.

## 11. Testing, debugging, and preventing loops

### Recommended sequence

1. Reproduce the issue with a minimal case.
2. Test one or two plausible hypotheses.
3. Locate the affected code.
4. Apply the smallest suitable change.
5. Run the specific test.
6. If it passes, run lint/type checks and wider tests in proportion to the risk.
7. Stop and summarize rather than launching more cycles without new evidence.

### Anti-loop prompt

```text
You have already attempted two changes without fixing the issue.
Do not repeat the same approach. Summarize the available evidence,
identify what contradicts the current hypothesis, and propose
the cheapest discriminating test before writing more code.
```

**Do not skimp on security, migration, or payment tests**: comprehensive validation may be necessary in these areas.

## 12. Everyday Claude Code commands

| Command | Purpose |
|---|---|
| `/model` | Check or choose a supported model |
| `/effort` | Adjust reasoning effort |
| `/usage` | Review usage, cache, and quotas depending on plan/version |
| `/context` | Inspect context usage |
| `/compact` | Summarize the current conversation |
| `/clear` | Start with a clean context |
| `/resume` | Resume a session |
| `/btw` | Ask a brief side question |
| `/mcp` | Inspect MCP integrations |
| `/agents` | Manage agents where supported |
| `/insights` | Analyze usage habits and friction points |
| `/rewind` | Manage checkpoints and restoration |
| `/diff` | Inspect changes |
| `/doctor` | Diagnose installation issues |

> Command availability may change between releases. If a command is not available, consult `/help` and the documentation matching your installed version.

## 13. Ready-to-copy prompts

### A. Universal optimization prompt

```text
Work in efficient professional-development mode.
Goal: maximum correctness with minimum unnecessary AI work.

1. Search files and symbols before reading code.
2. Read only relevant sections; avoid complete dumps.
3. Do not repeat completed searches or tests without justification.
4. Prefer deterministic local commands for mechanical analysis.
5. Reuse existing patterns and dependencies.
6. Avoid unrelated refactoring and unnecessary agents.
7. Apply a focused patch and perform targeted checks.
8. If two similar attempts fail, reassess the diagnosis.
9. Keep output, logs, and final reports concise.
10. Never compromise security, compatibility, or essential tests.

At the end, report changed files, validations performed,
outcomes, and outstanding risks.
```

### B. New feature

```text
Implement [FEATURE] within the existing architecture.
First look for reusable components and provide a plan of no more
than five points. Then implement without touching unrelated areas.
Run relevant tests and provide a short summary.
```

### C. Bugfix

```text
Fix [BUG]. Reproduce the behavior, locate the affected files
with targeted searches, verify the cause using the cheapest
relevant test, and apply a minimal fix.
Do not read the entire repository or try random changes.
```

### D. Read-only review

```text
Perform a READ-ONLY review of [AREA].
Do not change files. Return only concrete findings ranked by
severity, with file/line, supporting evidence, and a proposed fix.
Avoid unverifiable speculation and duplicates.
```

### E. Handoff to a new session

```text
Prepare a transferable summary of no more than 350 words:
goal, decisions, affected files, implemented patches,
tests, open issues, risks, and the exact next action.
No verbose history or discarded hypotheses.
```

## 14. Realistic scenarios: WordPress, Electron, TypeScript

### Scenario 1 — Slow WordPress plugin

**Inefficient request:** “Analyze the entire site and optimize the plugin.”

**Professional request:**

```text
In WordPress plugin [NAME], the admin page takes six seconds.
Focus on admin_init/admin_menu hooks, SQL queries, and HTTP calls.
Locate files using text searches, determine which functions run
when opening the page, and fix only the confirmed bottleneck.
Preserve sanitization, nonces, and permission checks.
Test the affected page and flag regression risks.
```

**Why it helps:** avoids involving unrelated frontend templates, translations, and modules. **Quality checks:** safe SQL, capability checks, nonces, PHP/WordPress compatibility, and before/after benchmarks.

### Scenario 2 — Electron: blank window on startup

```text
The Electron window is blank on Windows after building.
First inspect the renderer console, preload, asset paths,
and base URL configuration. Examine only package.json,
Electron/Vite configuration, and related bootstrap files.
Propose one leading hypothesis and a discriminating test.
Do not reinstall all dependencies without evidence.
```

**Why it helps:** reduces repeated installations, random exploration, and long rebuild cycles. **Tests:** build, launch the actual packaged application, and inspect renderer/main logs.

### Scenario 3 — TypeScript: 200 errors after refactoring

**Do not** paste 20,000 lines of compiler output.

```powershell
npx tsc --noEmit --pretty false 2>&1 | Select-String 'error TS' | Select-Object -First 60
```

Prompt:

```text
Group TypeScript errors by root cause.
First identify the two or three types or modules responsible
for the largest number of errors. Fix the shared cause,
then compile again. Do not mechanically fix 200 errors
one by one.
```

**Why it helps:** a few upstream problems often cause many cascading errors. If the first 60 results are unrepresentative, calculate a distribution by error code without feeding the full log into the model.

### Scenario 4 — Large new feature

1. Session A: define requirements, risks, and a concise plan.
2. Record decisions in a short project file.
3. Session B: implement one concrete component or milestone.
4. Run targeted tests, commit, and summarize.
5. Session C: integrate and run regression tests.

**Why it helps:** more focused histories, fewer conceptual conflicts, and a natural point to use `/clear`. Do not arbitrarily split tightly related work that benefits from shared context.

### Scenario 5 — Investigation in a monorepo

A cheaper subagent searches for billing-module references across packages and returns a map of ten files. The main agent inspects only the three critical ones. This makes sense when exploration is substantial; otherwise, one `rg` command is simpler.

## 15. A complete professional daily workflow

### Start of the day — two minutes of preparation

- Open the correct repository and check Git status.
- Confirm the model with `/model` and reasoning level with `/effort`.
- Review applicable `CLAUDE.md` instructions and essential MCP integrations.
- Define a specific task and completion criteria.

### During development

**Recommended cycle:**

```text
Defined task
    ↓
Targeted file search
    ↓
Diagnosis / short plan
    ↓
Minimal change
    ↓
Relevant test
    ↓
Result and commit
```

When context grows: `/context` → `/compact` if appropriate. When switching tasks: save a handoff → `/clear`.

### End of the day — five minutes

- Review `/usage` and note anomalies.
- Check `git diff` and test results.
- Save important technical decisions in the repository.
- Occasionally consult `/insights` for recurring sources of wasted work.

## 16. Measuring results, quotas, and savings

**Do not compare completely different sessions.** Compare similar tasks while holding result quality constant.

### Measurement sheet

| Metric | Before | After | Notes |
|---|---:|---:|---|
| Tasks completed correctly | | | |
| Model requests/retries | | | |
| Input tokens | | | If visible |
| Output tokens | | | If visible |
| Cache reads/misses | | | If supported |
| Remaining plan quota | | | Varies by plan |
| Total task time | | | Include testing |
| Bugs or regressions | | | **Must not increase** |

### Practical A/B approach

1. Select three similar development tasks.
2. Complete one comparable group using your usual workflow.
3. Complete another comparable group using this guide.
4. Record usage, time, passed tests, retries, and problems.
5. Keep only optimizations that improve efficiency **without reducing quality**.

On Pro/Max subscriptions, a displayed monetary equivalent for a session may not be an actual charge. Refer to plan usage indicators and official billing information.

## 17. What NOT to do: false optimizations

| False trick | Why it is unreliable | Better alternative |
|---|---|---|
| “You will definitely save 90%” | No universal reduction is guaranteed | Measure comparable tasks |
| Always use minimum effort | Can increase mistakes and retries | Match effort to complexity and risk |
| Compact every five messages | Overhead, loss of detail, and cache rebuilding | Compact when beneficial |
| Always clear context | Discards useful information and cache reuse | Clear when switching tasks |
| Ten agents for every task | Every agent consumes tokens | Delegate only substantial work |
| Disable all tests | Apparent savings, expensive regressions | Focused tests plus risk-based regression |
| Filter errors until they disappear | Leads to incorrect diagnoses | Expand output when needed |
| Put every detail in CLAUDE.md | Persistent context overhead | On-demand skills and targeted documents |
| External router = free tokens | Routing does not eliminate model costs | Check terms, quotas, compatibility |
| Proxy subscription credentials without checking rules | Potential conflict with provider terms | Read provider-specific conditions |

## 18. Operational checklists

### Before starting

- [ ] I have defined the exact requested change.
- [ ] I have identified what must NOT change.
- [ ] I have selected an appropriate effort level.
- [ ] I have checked the repository, Git state, and test commands.
- [ ] I have disabled unnecessary integrations where appropriate.

### During the task

- [ ] Claude searches before reading whole files.
- [ ] It is not repeating identical investigations.
- [ ] It is not dumping enormous logs.
- [ ] Changes are limited to relevant files.
- [ ] Tests are meaningfully connected to the patch.
- [ ] I am stopping loops that make no progress.

### Before finishing

- [ ] I have inspected the changes (`/diff` or `git diff`).
- [ ] Important tests have run.
- [ ] Limitations and open issues have been documented.
- [ ] The final summary is short and verifiable.
- [ ] I have recorded decisions needed for the next session.

## 19. Ready-to-use CLAUDE.md template

> Copy **only the following block** into your repository's `CLAUDE.md` file. Customize the bracketed fields.

```markdown
# Project Instructions

## Project
- Stack: [TypeScript / Electron / WordPress / PHP / other]
- Main directories: [src/, tests/, ...]
- Package manager: [pnpm/npm/composer]
- Relevant commands: [lint, typecheck, test, build]

## Engineering quality
- Follow existing architecture and coding conventions.
- Prefer small, focused changes and existing dependencies.
- Preserve public APIs unless the task explicitly requires changes.
- Protect secrets, access control, input validation and data integrity.
- Do not silently alter unrelated behavior.

## Efficient working method
- Search paths and symbols before reading files.
- Read only relevant code sections.
- Avoid generated files, dependency directories and old logs unless relevant.
- Do not repeat completed investigations without new evidence.
- Prefer local deterministic commands for mechanical processing.
- Use focused tests first; expand coverage according to risk.
- Avoid spawning agents for trivial tasks.
- Stop and reassess if repeated attempts fail.
- Keep tool outputs and final explanation concise.

## Verification
- Run the relevant tests for every functional change.
- For security, payments, migrations and releases, perform appropriate
  additional validation; never trade off safety to save tokens.
- State explicitly when tests cannot be run.

## Final response
- Summary of changes
- Files affected
- Tests run and results
- Remaining risks or next steps

## Compact handoff
When summarizing context, preserve objective, decisions,
changed files, tests, blockers and exact next action.
Omit obsolete investigations and verbose logs.
```

**Practical tip:** keep the complete guide outside `CLAUDE.md` and place only essential operating rules in that persistent file. Putting the entire manual inside `CLAUDE.md` would undermine the efficiency you want to gain.

## 20. Glossary and official sources

### Essential glossary

- **Token:** unit of text/information processed by the model.
- **Context window:** how much information a request can include.
- **Prompt cache:** efficient reuse of previously processed content.
- **Cache hit/miss:** successful reuse / failure to reuse a cached prefix.
- **Compaction:** a summary that replaces part of a lengthy history.
- **Subagent:** an agent with an isolated context for a specific task.
- **Agent team:** multiple collaborating agents, potentially increasing usage.
- **MCP:** protocol for integrating external tools and services.
- **LSP:** structured support for symbols, definitions, and code diagnostics.
- **Hook:** event-triggered automation, often running without an LLM.
- **Effort:** control over reasoning depth on supported models.

### Official primary sources

- Anthropic — **Manage costs effectively**: https://code.claude.com/docs/en/costs
- Anthropic — **Best practices for Claude Code**: https://code.claude.com/docs/en/best-practices
- Anthropic — **Model configuration**: https://code.claude.com/docs/en/model-config
- Anthropic — **Commands**: https://code.claude.com/docs/en/commands
- Anthropic — **Features overview**: https://code.claude.com/docs/en/features-overview
- Anthropic — **Settings / environment variables**: https://code.claude.com/docs/en/settings

**Future-proofing note:** Claude Code evolves rapidly. Features, effort levels, cache statistics, and commands may require a minimum version or change in later releases. Periodically review the official documentation and your client's `/help` screen.

---

### Final reminder

> **Maximum efficiency does not mean forcing Claude to think less in every situation. It means preventing it from repeatedly reasoning about the wrong things, the wrong files, and outputs that a local tool can already process.**

*End of guide — Version 1.0 (English edition).*
