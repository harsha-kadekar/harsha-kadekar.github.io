---
category: Technical
date: 2026-09-19
layout: post
tags:
- llm
title: Notes On Learning to Code With LLMs - 2026-09-11
updated: 2026-09-19
---

## Overview

This is the third post ([first](https://www.harsha-kadekar.blog/notes-on-learning-to-code-with-llms-2026-02-15.html), [second](https://www.harsha-kadekar.blog/notes-on-learning-to-code-with-llms-2026-02-26.html)) in my attempt to learn how to use LLMs for coding. How we write code is changing, as are the tools and processes we use to solve problems. Even though the basic structure of problem-solving remains the same, the approach is evolving. For me, a primary way of understanding a system and its solution is shifting from writing code toward requirements gathering, design, and review. I use `Claude` as a coding, research, and design agent, and `Codex` as my primary review agent. One of the biggest changes is that I have stopped using IDEs or GUI code editors. I work in the terminal most of the time, with `Claude` and the Helix terminal editor as extensions of that workflow. Skill files can help agents follow acceptable software-engineering best practices. However, agents still require oversight of both what they do and what they produce. Running agents therefore requires time and mental energy.

## Experience

As of September 2026, through a technology allowance at work, I can spend and be reimbursed up to $50 each month for personal AI use, including courses, subscriptions, and tools. I use it for `Claude` Pro and `Codex` Pro subscriptions. I use `Claude` for most coding activities and `Codex` for reviews. After four months of use, I would still subscribe to `Claude` Pro even without the allowance, along with a lower-priced `Codex` plan, if one were available. (There was an $8 plan earlier, but it seems to have been removed - bummer.) This is not because `Codex` has quality or experience issues; it is solely due to my usage pattern. Because I use `Codex` mainly for reviews rather than implementation, I use it less often. At $20, it currently feels overpriced for my usage.

I rely on skills for recurring workflows; I am creating more of them at work as well. Here are some examples:

- I created a `Claude` skill called [`fix-github-issue`](https://github.com/harsha-kadekar/citta/blob/master/.claude/skills/fix-github-issue/SKILL.md) for working on a GitHub issue. Given an issue link, it first researches the problem and explicitly presents its plan of action. After I approve the plan, it implements the solution using test-driven development. It then runs analysis and tests, refactors the code, runs `/code-review`, asks `Codex` to review the work, and fixes the findings. It waits for my review before creating a PR, then waits for the PR checks to pass and reports back. This workflow gives me strong control while helping generate quality code.
- I created other skills, such as `flutter analyze` and `flutter test`, which are used within `fix-github-issue`. I installed `Flutter` in a custom location, so each time the agent ran static analysis or tests, it had to search for the Flutter and Java paths. These skills keep those paths available, so the agent does not need to repeat the search every time.
- I also created `weekly-review` and `monthly-review` skills for my personal reviews. For `weekly-review`, the agent goes through daily notes, calculates the core-habits score, lists what I did and missed against my plan, compares the result with the previous week's review, and produces a draft review. I then select items and add my own reflections. Similarly, `monthly-review` goes through that month's weekly reviews, calculates the core-habits scores, lists what I did and missed against the plan, compares the result with the previous month, and prepares a review based on its assessment.

There are a few `Claude` commands that I use frequently, both at work and in personal projects:

- `/code-review` - I run this whenever there is a code change. It catches regressions and other issues well. Running a review in `Codex` sometimes provides fresh findings beyond what `/code-review` catches.
- `/remote-control` - I can start a GitHub issue fix on my laptop and follow its progress from my phone while playing with my kid or doing household work. It lets me provide approvals from mobile without investing sustained focus - just occasional checks for approval requests.
- `/clear` - Rather than using `/exit` and starting a fresh `Claude` session, this resets the session for a new task.
- `plan mode` - At the beginning of a project or when I need to find a solution to a problem, I need to investigate and ask questions. This mode streamlines that process.

In the “What next?” section of my [previous post](https://www.harsha-kadekar.blog/notes-on-learning-to-code-with-llms-2026-02-26.html), I wanted to:

- *Develop skills that bring software-engineering best practices into my workflow*. I feel I have been able to do this successfully: the workflows above automate recurring work while retaining approval and review steps. I will discuss some observations about them later.
- *Learn how an LLM agent can augment a developer.* My continued experience suggests that this is true. However, I think some skills are universally useful while others are specific to an individual developer. I still do not know the right balance between them.
- *Explore better code-review tools.* Unfortunately, I have not found anything better in this space, although I have not explored it deeply. For now, I rely on `git status`, `git diff`, and an agent summary because they let me inspect the working tree, review the changes, and compare that evidence with the agent's account of its work.

## Critical Observations

Until recently, my usual software-development cycle was: requirements gathering and problem understanding → solution design → implementation (tests and logic) → review → shipping. Each stage influences the others, and implementation often reshapes the design.

By going through that entire cycle myself, I developed a clear picture of what I had built and how the system should behave. That understanding gave me a foundation for debugging issues, maintaining the system, and adapting it to new problems.

LLM agents now take on much of the implementation phase. They can also contribute substantially to solution design and, to a smaller extent, to problem understanding and review. But they do not remove a developer's responsibility to debug, maintain, and evolve the system. Since implementation used to be a major way I gained that understanding, I now need to build it more deliberately through problem understanding, requirements gathering, solution design, and review.

- I still need to understand the domain and the programming language well enough to steer LLMs in the right direction. It is like exercising - not because I do a lot of physical work, but to stay healthy. Similarly, I may need to write code regularly without using an LLM, simply to maintain the habit and understanding required to steer one well.
- Deciding what to delegate to an LLM and what to think through myself is difficult. Delegating too much risks dulling my ability to evaluate designs, diagnose failures, and make trade-offs independently. Finding that balance is critical.

## What next?

Here are some of the things I would like to practice and learn next:
- Improve my `Ghostty + Zellij + Helix + Claude` setup. I want to spawn subagents in `Claude` and manage panes and tabs within Helix, Zellij, and Ghostty.
- Explore plan mode more deeply for a project or task. I want to invest time in understanding the problem, devising a solution, and breaking it into smaller tasks before spawning multiple agents. My effort should then focus mostly on finding the solution - both the algorithm and its implementation - and reviewing the design, tests, code, and execution.
- Learn to track multiple sessions and manage subagents more effectively in `Claude`.
- Develop a way to practice `Java`, `Go`, and `Python` through coding katas so that I retain coding muscle memory.
- Explore ways to improve the review phase.

---
- I have used LLM agents to review the draft, help with rewording and rephrasing sentences, and do research.