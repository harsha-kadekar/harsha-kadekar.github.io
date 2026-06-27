---
category: Technical
date: 2026-06-20
layout: post
tags:
- setup
- obsidian
title: My Obsidian Settings
updated: 2026-06-20
---

I use [Obsidian](https://obsidian.md) to capture notes, thoughts and tasks. In this post, I want to note down the settings I use in Obsidian so that, next time I configure a new system, I can just reference this.

My operating system is [Ubuntu](https://ubuntu.com/download/desktop). So, these instructions are specific for that operating system.

## Installation

Install Obsidian by downloading the deb file from https://obsidian.md/download. Sometimes, the Obsidian Web Clipper does not work with the one installed from the snap/Ubuntu Software. Hence, install it using the deb file directly.

## Settings

These are the settings. I'm only listing settings that differ from the defaults.
- General
	- Log in to get the Catalyst license
	- Enable `Command Line Interface`
	- Enable `Receive Early Access Versions`
- Editor
	- Spell Check Languages
		- English (United States)
	    - English (United Kingdom)
	    - Hindi
- Files and Links
	- Default location for new attachments: `In the folder specified below`
	    - `Attachments`
	- Automatically update internal links: `True`
- Appearance
	- Theme: I change it after every few days. I can start with `Minimal`
	- Disable `Inline Title`
- Core Plugins
	- Following core plugins are switched off
	    - Audio Recorder
	    - Publish
	    - Random Note
	    - Slash Commands
	    - Slides
	    - Sync
	    - Unique Note Creator
	    - Workspaces
- Community Plugins
	- Turn off Restricted Mode
	- Enable `Automatically Check for Plugin Updates`
	- I use following community plugins
		- Advanced Tables
	    - Automatic List Management
	    - Calendar
	    - Charts
	    - Dataview
	    - Excalidraw
	    - Git
	    - Homepage
	    - Reminder
	    - Tag Wrangler
	    - Tasks
	    - Templater

## Core Plugin Settings

### Daily Notes
- New file location: `DailyNotes`
- Template file location: `Templates/Template_DailyNotes`
- Date format: `YYYY-MM-DD`

### Templates
- Template folder location: `Templates`

## Community Plugin Settings

Apart from the ones listed below, remaining plugins (Advanced Tables, Charts, Dataview, Excalidraw, Reminder, Tag Wrangler, Tasks) work well with their default settings.

### Automatic List Management
- Turn off: `Auto Sort On Changes`

### Calendar
- Words Per Dot: `2048`

### Git
- Auto commit-and-sync interval: `60`
- Auto commit-and-sync after stopping file edits: `On`
- Pull on startup: `On`

### Homepage
- Turn on `Pin`
- Homepage view: `Reading View`

### Templater
- Template folder location: `Templates`

## Related Posts

- [My Personal Laptop Setup](https://www.harsha-kadekar.blog/my-personal-laptop-setup.html)
- [My Obsidian Vault](https://www.harsha-kadekar.blog/my-obsidian-setup.html)
- [My Development Configuration](https://www.harsha-kadekar.blog/my-development-configuration.html)

---