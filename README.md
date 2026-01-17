# Example Setup

A project configured with a few Claude Code skills and example CLAUDE.md file just to illustrate a few things you can do.

## Claude Code Best Practices

**Start simple, and incrementally, methodically build**
* I'd start with the things that don't change production code (safe) but add value, e.g. test authoring, code reviewing, architecture planning, etc
* Have a lightweight, incremental test & rollout process (e.g. 1-2 people try some tools, find a couple worth bringing to the team, install them team-wide & test for a week, then decide whether / how to incorporate them into the process
* As you get into letting your agent write code, start with smaller tasks (e.g. bug fixes, do first draft of a new feature, etc)

**Think of Claude Code as a junior programmer that you need to teach over time**
* When CC goes off track, add to its knowledge (via CLAUDE.md, skills, etc) and it will improve.
* At first it will fail at various things, but keep "training" it. Tiny changes compound over time and it gets much better.
* There will be some things it's just not good at, that's ok just keep doing those yourself

**Teach Claude Code over time but be sparing in context:**
* Have a very opinionated `CLAUDE.md` about what you want / don't want in your code base.. BUT:
- Keep your `CLAUDE.md` files VERY concise - it's sent with every turn of your conversation. Every once in a while I prune mine to remove non-essentials.
- Use `~/.claude/CLAUDE.md` for global preferences
- You can @ embed files in CLAUDE.md so they get auto-loaded ... good way of combining personal rules with shared team rules

**Planning is now where the real work happens**
* Spend more time planning than executing — results are noticeably better and execution is much fastor
* Use a dedicated planning skill -- I love the brainstorm skill (taken from superpowers), it's my preferred method right now. But claude code plan mode does a pretty good job. I like ones where the agent challenges you and interviews you to get to an answer (I have a spec-interview skill I'm testing out right now also)
* Side effect: agentic coding makes you a better architect because you can't skip the planning phase anymore

**Other ways to increase the success rate once you let your agent code:**
- Break large tasks into smaller, trackable units and assign one at a time -- it does better when the task is discrete & small. A simple to do list in a markdown file with a reference spec does a good job, I'd start with that but if you get complex dependency chains you could consider an agentic issue tracker (I use beads, used to use taskmaster)
- As part of your standard workflows, have it run standard quality checks (lints, automated tests) after every task is complete, it'll debug & fix its own issues
- Use skills for complex workflows. Claude code is **really** good at following long instruction sequences and you can embed custom scripts in skills which is really powerful
- Try to do most of your work in the first half of filling up the context, it gets dumber as the context fills up. I like to clear context and re-prime it between tasks / features

**Quality engineering is maybe the most important investment in an agentic coding world**
* This includes standard QE stuff (e.g. test coverage + gap detection, pre-release scan hooks, ability to roll back deploys, etc), as well as agentic tools like agentic code reviews, etc. There are some off the shelf PR review tools like coderabbit & greptile, I haven't tried them personally yet and just use my own.
* Any time something slips through (even if it didn't get far) I think about what I can add to engineer that class of problems out of existence. Over time the system becomes extremely robust.

**Testing philosophy matters more than ever**
* I like the testing trophy approach: heavy on integration tests, light on unit tests. Care if the system works, not if a function returns expected output, and ideally tests survive most refactors
* This matters because Claude writes whatever tests you let it write. Without strong opinions baked in, you get unit tests that test implementation details instead of actual behavior—or worse, tests that validate mock behavior over app behavior.

**Proceed with caution re: permissions**
* I recommend being very conservative with permissions -- claude code is an agent that is really good most of the time can sometimes do VERY stupid things. Don't give it the ability to do anything destructive.
* My approach: start with no permissions and gradually curate approved permissions in ~/.claude/settings.json that you are comfortable with so it speeds things up (e.g. approve something then move the generalized version from your project's settings.local.json into your user-level settings). It's a pain at first to be approving every time but it speeds up and I like the comfort of knowing I've thought about all the approvals up front
* I also would always run in a sandbox for extra safety (either the built in /sandbox mode or a dev container of some sort, there are several good options).
* I also never store any important credentials in .env files, I'll just ref a 1password entry so the runtime pulls down any needed passwords so I don't have to worry about my coding agent seeing those credentials.

**Skills are really powerful and can help avoid context bloat**
- Use well-designed skills for repeat tasks with progressive disclosure -- gives significant capabilities but sparing in context usage
- You can configure skills to fork context, so the work they do doesn't pollute the main context
- You can also set them up to act as slash commands (human initiated) or not (so they're available for the agent or other skills but don't pollute your command list)
- Claude code offers a set op
- ***NOTE:** I'm stopping 3rd party plugins other than the claude code official ones because I don't want to update one day and introduce malicious code. I have a skill that copies down a remote skill from the git repo so I control what gets into my skill set. It stores a reference to the original source so I can pull down updates on demand later.*




## Skills

### agent-browser

CLI browser automation using Vercel's headless browser. Uses ref-based element selection (@e1, @e2) from accessibility snapshots for AI-friendly web interaction.

**Key commands:**
- `agent-browser open <url>` - Navigate
- `agent-browser snapshot -i` - Get interactive elements with refs
- `agent-browser click @e1` / `fill @e2 "text"` - Interact using refs
- `agent-browser screenshot` - Capture viewport

### brainstorming

Collaborative design process for turning ideas into specs. Explores context, asks questions one at a time, proposes 2-3 approaches with trade-offs, then presents designs in 200-300 word sections for incremental validation.

**Process:** Context -> Questions -> Approaches -> Design sections -> Documentation

### frontend-design

Creates distinctive, production-grade frontend interfaces that avoid generic AI aesthetics. Emphasizes bold typography choices, cohesive color themes, meaningful motion, and unexpected spatial composition.

**Focus areas:** Typography, color/theme, motion, spatial composition, backgrounds/visual details

### condition-based-waiting

Eliminates flaky tests by replacing arbitrary timeouts with condition polling. Core principle: wait for actual conditions, not guesses about timing.

```typescript
// Instead of: await sleep(500)
await waitFor(() => getResult() !== undefined);
```

### writing-tests

Behavior-focused testing using the Testing Trophy model. Prioritizes integration tests with real dependencies over mocks.

**Priority:** Integration (default) > E2E (user workflows) > Unit (pure functions)

**Only mock:** External APIs, time/randomness, third-party services

## Setup

```bash
task setup
```
