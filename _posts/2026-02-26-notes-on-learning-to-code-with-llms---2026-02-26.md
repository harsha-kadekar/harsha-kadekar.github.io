---
category: Technical
date: 2026-02-26
layout: post
tags:
- llm
title: Notes On Learning to Code With LLMs - 2026-02-26
updated: 2026-04-25
---

## Overview

This is the 2nd post ([first one](https://www.harsha-kadekar.blog/notes-on-learning-to-code-with-llms-2026-02-15.html)) on my attempt to learn how to use LLMs for coding. I developed an Android app - [Citta - A Personal Meditation Tracking App](https://www.harsha-kadekar.blog/citta-a-personal-meditation-tracking-app.html) using Claude Code, even though I had never worked with Dart, Flutter, or Android development before. In the process of development, I realized that the essential software development engineering skills remain the same even in the LLM era of coding. LLM agents can produce professional-looking apps very fast, but making the underlying code production-ready and maintainable still takes work. LLMs/Agents will supercharge you if you have deep domain knowledge, use good software engineering practices, and have good basic computer science knowledge. Let me explain this in detail.

## Experience

With my zero knowledge of Android (or its SDK, or Flutter framework), I was still able to develop a good app within 2 weeks (~30 hours of actual development work). The developed app is comparable to equivalent professional apps listed in the Play Store. Using an LLM definitely reduced the overall turnaround time from idea generation to the first working product.

I started by using the planning mode of Claude Code (`shift + tab`). I interacted with Claude Code to discuss my idea for the app. I explained how my app should look and feel, and what features the app should provide. As part of this process, I did ask some questions like which framework I should use, what kind of storage I should explore, why a DB does not make sense here, what the effect of storing everything in a file would be, and how this would scale as years go by. For everything, Claude gave me a good explanation and then followed up with a couple of options marked with the preferred way to do it. For a few of them, I chose what Claude gave as preferred, and for others, I overrode the preferred way with something else that I thought was the right way to do it. If I had prior knowledge in Flutter or Android development, I could have led Claude in an even better direction, as I could have asked better questions. With that domain knowledge, I would have thought even more deeply about the internals, and thus probably it would have given better alternatives. 

I asked Claude to break the requirements into atomic small tasks that could be worked on independently. It did break them down into smaller tasks. I wanted to go one task at a time. But I guess my prompt was not clear, and Claude Code went ahead and completed all the broken-down tasks at once. Claude developed the complete UI. The UI development was a breeze with little hands-on help. As it completed everything, a lot of code got generated. I had to spend 2-3 days reading the code to understand what it had written. So, even though I was progressing fast in app development, which was exciting, I had also lost the context of what it was doing underneath. I had to slow down to regain an understanding of what it was doing so that I would be comfortable with what I was shipping.

Overall, it did not follow good coding best practices. It had duplicated code and also very little test coverage. Much of the implemented code did not have tests. I had to explicitly ask it to add test cases. So, even though the app looked professional from the outside, the code underneath was not production-ready or maintainable.

I wanted Claude to complete one atomic task at a time, then come back to me so that I could review it and then go to the next step. I also wanted it to add those tasks as GitHub issues so I could track the progress of the product implementation. Claude Code, in a few instances, pushed code to GitHub without running all the tests and static analyzers. Ideally, the iteration would be: implement a single task, run the unit tests, run the analyzers, do a self-review, wait for my review, push it to GitHub after human review, mark that task as complete in GitHub, and finally move on to the next GitHub issue.

There were many things Claude did not remember in its context, and it kept on making the same mistakes. For example, I had installed the Flutter SDK in a custom folder. Even though I provided the actual location of the SDK when it failed the first time, it did not remember. Rather, it kept on making the same mistake when it tried to run the build, as it could not find the SDK in the standard location. I created a skill which helped reduce that repeated mistake.

There was one bug related to the alarm not playing the first time the app started. Claude tried many things to fix it, but failed. Those fixes made things worse, and I had to roll back those changes. I did some investigation on my own, and I found two links which had information and fixes about a similar problem. I suggested those two links to Claude Code, and based on that, it implemented the actual fix for the bug. This worked nicely! Probably LLMs are good at solving bugs that need relatively little context. In this case, it needed to search for similar problems/errors and then infer how it could apply that knowledge to the current problem.

Claude Code had introduced a few logical bugs while developing the app. For example, the way it had implemented file backup and recovery had issues that could have led to loss of data. Only when I read the code was I able to discover and fix it. From this, I feel we need strong domain knowledge or experience which would help identify and fix these problems outside of the LLM agents. Having closer review cycles of generated code will also help identify them early and fix them.

The other thing I missed was a better code review tool. I would want to see the LLM prompts that generated or updated the code along with the code it had generated. This would give better context. So, the review should capture both code and LLM prompt interactions.

## What next?

Here are some of the things I would like to practice and learn next:
- Developing skills or rules for the LLM agent that would help bring software engineering best practices into the workflow, so that LLM agents work through atomic tasks in a test-driven development style with a close review cycle.
- An LLM agent needs to augment the developer, and hence what I expect from the agent will be completely different from what another developer seeks from agents. I would want to set the following rules for the LLMs to be effective for my way of development:
	- Do not implement more than one GitHub issue without approval.
	- Run formatter, analyzer, and tests before reporting completion.
	- Avoid duplicate code.
	- Do not push to GitHub unless explicitly approved.
	- Start with test-driven development for every GitHub issue.
	- Add or update tests for every behavioral change.
	- Do a code review of self-implemented code before declaring the task completed.
	- Record unresolved risks before moving to the next task.
- Explore better code review tools that can show both the generated code and the LLM context that produced it.

## Critical Observations
- Using an LLM agent for a new product idea can drastically reduce the overall time for actual product development. But there is a real risk of losing an understanding of the underlying code of the product. So you need to slow down to bring yourself up to speed.
- Writing code via LLMs does not remove my responsibility to read the generated code to understand the in-depth context.
- We need to have in-depth context of the problem/domain as well as coding/computer science knowledge for better prompts and a better way to lead the agents in the right direction.
- I need to create LLM agent skills or rules to make the code style and quality closer to the way I would have written it.


---