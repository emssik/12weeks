---
description: Generates a 12-week plan based on filled planning form
argument-hint: <path-to-filled-form>
---

# Generating 12-Week Plan

<prerequisites>
First, run `date +%Y-%m-%d` to get today's date. Use this date to calculate the 12-week period start and end dates, and to determine the correct quarter for the output filename.
</prerequisites>

<why>
The user needs a concrete, realistic 12-week plan. The plan must be achievable, not perfect. Overly ambitious plans lead to abandonment - better to do less and actually complete it.
</why>

<validation>
BEFORE generating the plan, check if project briefs exist for all projects mentioned in the form.

1. Read the filled form and identify all projects/goals
2. For each project, check if a brief exists in `projects/[project-name].md`
3. If ANY brief is missing:
   - List which briefs are missing
   - Tell the user to fill them using `templates/project-brief.md`
   - DO NOT generate the plan - stop here
4. If all briefs exist but are incomplete (missing key sections like "Current state", "Stages"):
   - List which briefs need completion
   - DO NOT generate the plan - stop here
</validation>

<sources>
Read all data sources in parallel, as they are independent:

<filled_form>
@$ARGUMENTS
</filled_form>

<context>
@context.md
</context>

<available_tasks>
@issues.json
</available_tasks>

<project_briefs>
Read ALL files from: projects/*.md
These contain the REAL information about each project: current state, tech stack, roadmap, stages.
</project_briefs>
</sources>

<task>
Based on the above data, generate a 12-week plan. Work systematically:

1. Analyze goals from the form and connect them with the vision from context.md
2. For each project, use ONLY the stages defined in its brief - DO NOT invent new tasks
3. Map brief stages to weeks, respecting:
   - Dependencies between stages
   - Complexity estimates from the brief (S/M/L/XL)
   - Blockers that need resolution first
4. Link tactics with existing tasks from issues.json where IDs match
5. Define milestones (week 4, 8, 12) based on brief stages, not arbitrary goals
</task>

<output_structure>
Save the plan to: `plans/12week-YYYY-QX.md` (e.g., plans/12week-2025-Q1.md)

The plan MUST contain these sections in this order:

## Summary
- Period: from-to
- 3 goals (one sentence each)

## Goal 1: [name]
### Tactics
| Week | Action | Related task (Linear) |
|------|--------|----------------------|
| 1 | [verb + what] | [ID or -] |
| 2 | ... | ... |

### Milestone week 4
[What should be done]

### Milestone week 8
[What should be done]

### Milestone week 12
[Success = ]

## Goal 2: [name]
[same structure]

## Goal 3: [name]
[same structure]

## Week model
[Time blocks based on schedule from context.md]

## Risks and mitigations
| Risk | Mitigation |
|------|------------|
| [from form] | [concrete action] |

## Rules
- Max 3-5 tactics per week total
- Buffer for unexpected events (emergencies, family)
- Mix difficult tasks with easier ones
</output_structure>

<guards>
## Why these rules matter

Plans filled with invented or vague tasks lead to overwhelm and abandonment. The briefs contain carefully thought-out stages - respect that work. A plan with gaps is honest; a plan with filler is harmful.

## Your role: optimizer, not inventor

You optimize HOW and WHEN things get done, not WHAT gets done. Think of yourself as a scheduler working with fixed inputs:

**Do this:**
- Arrange stages from briefs into optimal weekly schedule
- Identify dependencies (stage B needs stage A first)
- Spot conflicts (two projects need same time block)
- Balance hard tasks with easier ones across days
- Flag when scope exceeds 12 weeks and suggest cuts
- Suggest parallel work where stages are independent

**Source of truth:**
- Tasks come ONLY from project briefs (projects/*.md)
- If brief says "Stage 1: X, Y, Z" - schedule X, Y, Z, nothing else
- If there's a gap between stages - leave the gap, don't fill it
- Generic tasks like "research", "plan", "prepare" only if explicitly written in brief

## Handling uncertainty

When something is unclear or missing from briefs:
- Ask the user directly: "[QUESTION: brief doesn't specify order of stages 2 and 3 - are they dependent?]"
- Mark gaps explicitly rather than guessing
- A plan with honest "[TBD]" markers is better than invented content
</guards>

<constraints>
Keep plans simple - complexity leads to abandonment. Realistic beats ambitious.

When the scope exceeds 12 weeks, say it directly and propose what to cut. Cutting scope is better than cramming - an achievable plan that gets 70% done beats an ambitious plan abandoned in week 3.
</constraints>

<methodology>
## 12-Week Year - Core Principles

**Fundamentals:**
- Max 3 goals per 12 weeks - better to do less and complete it than more and abandon
- Each goal must have a "why" (connection to vision from context.md)
- Don't change goals during the 12 weeks - only tactics

**Milestones (checkpoints):**
- Week 4: first checkpoint - are we on track?
- Week 8: second checkpoint - adjust tactics if needed
- Week 12: final evaluation - goal achieved? partially? not at all?

**Week model:**
- Define time blocks for types of work (based on context.md)
- Account for fixed calendar commitments
- Max 3-5 tactics per week total (not per goal!)

**Agent's role:**
| When | What to do |
|------|------------|
| Plan generation | Distribute tactics across weeks, identify dependencies, flag risks |
| Weekly | Remind about review, extract tactics from plan |
| Every 4 weeks | Initiate mini-review, signal at-risk goals |
| End of 12 weeks | Conduct evaluation, help plan next cycle |
</methodology>
