---
name: dynamic-multi-agent-workflow
description: Use this skill for complex human-delegated work that requires dynamic task decomposition, multiple agents, quality review, and owner-based revision. Do not use for simple questions or quick answers.
version: 1.0.0
author: Jim
metadata:
  hermes:
    tags:
      - multi-agent
      - workflow
      - task-decomposition
      - quality-control
      - revision-loop
      - project-management
---

# Dynamic Multi-Agent Workflow

## Purpose

This skill helps Hermes complete complex human-assigned work through a dynamic multi-agent workflow.

The goal is not to answer immediately, but to act like a project manager:

1. Understand the human's full request.
2. Convert the request into a clear task brief.
3. Dynamically decide what agents are needed.
4. Assign subtasks to the right agents.
5. Run agents in parallel when possible.
6. Collect all outputs.
7. Review completeness and quality.
8. Return failed parts to the original responsible agent.
9. Deliver the final result only after the work passes review.

## When to Use

Use this skill when the task is:

- complex
- multi-step
- high-stakes
- project-like
- requires research, writing, coding, deployment, analysis, or planning
- requires several independent parts to be completed
- requires quality control before final delivery
- likely to benefit from parallel agent execution

Examples:

- Build a full deployment plan
- Create a business workflow
- Write a long report
- Research and compare multiple options
- Generate a full website or application plan
- Complete a technical troubleshooting project
- Produce a presentation structure with speaker notes
- Analyze several documents and synthesize a final answer

## Core Principle

Do not use a fixed set of agents.

The Master Agent must dynamically decide:

- how many agents are needed
- what each agent should do
- what capability each agent needs
- whether tasks should run in parallel or sequentially
- what dependencies exist between tasks

The agent team must be created based on the specific task, not from a fixed template. Before the task start, the Master Agent has to make sure what types of agent should be used.
Once confirmed, the agent team should remain stable; do not re-plan the team mid-execution unless the Review stage proves a subtask cannot be owned by any existing agent.

## Required Workflow

### Stage 1: Understand the Human Request

The Master Agent must extract:

- original user request
- final goal
- detailed requirements
- constraints
- expected output format
- quality standards
- deadline or priority if provided
- missing information if any

If missing information blocks the task, ask the human.
If missing information does not block the task, ask the human whether they want to add anything.

### Stage 2: Create a Task Brief

Before delegating, create an internal task brief:

```markdown
# Task Brief

## Original Human Request
...

## Final Goal
...

## Requirements
- ...

## Constraints
- ...

## Expected Output
...

## Quality Standards
- ...

## Assumptions
- ...

## Subtasks
1. ...
2. ...
3. ...

```

### Stage 3: Dynamic Agent Planning

The Master Agent must decide the agent team dynamically.

For each agent, define:
```markdown
## Agent Assignment

### Agent ID
agent-01

### Role
...

### Subtask
...

### Required Context
...

### Expected Output
...

### Quality Criteria
...

### Dependencies
...
```

Important rules
* Do not create unnecessary agents.
* Do not split work only for the sake of splitting.
* Prefer parallel work when subtasks are independent.
* Use sequential execution when one subtask depends on another.
* Each agent must have a clear owner responsibility.

### Stage 4: Agent Execution

Each task agent must return:

```markdown
# Agent Output

## Agent ID
...

## Assigned Task
...

## Completed Work
...

## Assumptions
...

## Limitations or Uncertainties
...

## Evidence / Reasoning / Operation Log
...

## Self-Check
- [ ] I completed the assigned task.
- [ ] I followed the required context.
- [ ] I met the quality criteria.
- [ ] I identified uncertainties clearly.

```

Agents must only complete their assigned tasks.
Agents must not silently expand scope unless necessary.

### Stage 5: Master Collection

The Master Agent collects all outputs and checks:

- every assigned agent submitted work
- every subtask has an output
- outputs do not conflict
- dependencies were respected
- missing information is clearly marked

### Stage 6: Review Agent Quality Check

Create a Review Agent only after execution.

The Review Agent must check two levels:

A. Subtask-Level Review

For each agent output:

```markdown
## Subtask Review

### Agent ID
...

### Pass / Fail
...

### Problems Found
...

### Missing Requirements
...

### Quality Issues
...

### Required Revision
...

```

B. Final Goal Review

Check whether the combined result satisfies the original human request:

```markdown
## Final Goal Review

- [ ] All human requirements are covered.
- [ ] The final result solves the original problem.
- [ ] No important detail is missing.
- [ ] The output format matches the request.
- [ ] The quality is good enough for delivery.
- [ ] Assumptions and limitations are transparent.

```

### Stage 7: Owner-Based Revision

If a problem is found, do not create a separate repair agent.

The Review Agent must identify:

- which subtask failed
- which original agent owns that subtask
- what exactly is wrong
- what must be changed
- what quality standard must be met

Then send the revision back to the original responsible agent.

```markdown
# Revision Request

## Return To
agent-XX

## Failed Area
...

## Problem
...

## Required Fix
...

## Context To Preserve
...

## Acceptance Criteria
- [ ] ...
- [ ] ...

```

The original agent must revise its own work because it already has the relevant context.

### Stage 8: Re-Review

After revision, the Review Agent must re-check only the changed part first.

Then the Master Agent must re-check the full combined result.

Repeat this loop until:

- all subtasks pass
- the final result passes
- or the Master Agent determines that the task cannot be completed without more human input

### Stage 9: Final Delivery

Only after review passes, the Master Agent may deliver the final result to the human.

The final answer must include:

- the completed result
- key assumptions if relevant
- unresolved limitations if any
- concise explanation of what was done

Do not expose unnecessary internal agent chatter unless the human asks for it.

## Failure Handling

If the workflow fails, the Master Agent must report:

```markdown
# Workflow Failure Report

## What Was Completed
...

## What Failed
...

## Responsible Agent or Subtask
...

## Why It Failed
...

## What Human Input Is Needed
...

```

## RULES
Hermes must prioritize:

1. correctness
2. completeness
3. context continuity
4. clear responsibility ownership
5. useful final output
6. avoiding unnecessary agent creation

Speed is secondary to quality for this workflow.