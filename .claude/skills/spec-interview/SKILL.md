---
name: spec-interview
description: This skill should be used when the user asks to "interview me about a feature", "help me spec out", "gather requirements for", "create a detailed spec", "ask me questions about what I want to build", "deep dive into requirements", or mentions wanting in-depth questioning about technical implementation, UI/UX, tradeoffs, or concerns before building.
---

# Spec Interview

Conduct rigorous in-depth interviews to extract comprehensive specifications through probing, non-obvious questions.

## Process

### 1. Gather Initial Context

**If spec file provided:** Read it completely, identify gaps and ambiguities to probe.

**If verbal description:** Ask for a brief summary of what's being built and the core problem being solved.

### 2. Interview Continuously

Use the **AskUserQuestion** tool repeatedly. Each round should ask 2-4 related questions.

**Question Philosophy:**
- Ask questions that challenge assumptions, not confirm them
- Probe for edge cases the user hasn't considered
- Force decisions on tradeoffs before implementation
- Avoid obvious questions (colors, fonts, minor details)

**Example probing questions:**
- "You mentioned X can be deleted - what happens to things that reference X?"
- "What if two users try to do this simultaneously?"
- "When these two requirements conflict, which wins?"
- "What happens when this fails halfway through?"

**Domains to cover** (adapt based on what's being built):
- Technical architecture and data model
- User flows and state transitions
- Error handling and edge cases
- Security and permissions
- Performance constraints
- Business rules and validation

### 3. Continue Until Complete

Keep interviewing until:
- Major domains relevant to the feature have been explored
- Key tradeoffs have been decided
- Edge cases for core flows have been addressed

Ask explicitly: "Are there areas that still feel unclear, or have we covered the key decisions?"

### 4. Write the Spec

After the interview is complete, write the spec to a file. Default: `SPEC.md` in current directory, or user-specified path.

Structure the spec based on what was discussed - no rigid template. Include:
- What's being built and why
- Key decisions made during the interview
- Technical details relevant to implementation
- Edge cases and how they're handled
- Any open questions that remain

## Key Behaviors

**Be a skeptical architect, not a yes-man.** The goal is to surface hidden assumptions before implementation begins.

**Don't ask permission to continue.** Keep interviewing until done - the user asked for an in-depth process.

**Adapt questions to context.** A CLI tool needs different questions than a web app. A solo project needs different questions than an enterprise system.
