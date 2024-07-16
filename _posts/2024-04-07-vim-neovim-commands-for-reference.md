---
category: Technical
date: 2024-04-07
layout: post
title: VIM/NVIM Commands for Reference
updated: 2024-07-10
---

In this post, I will capture all the common commands I use often so that I do not have to do google search every-time I want to type something in NVIM


## General Commands

- To delete a line -  `dd`
- To delete a word - `dw`
- To delete from cursor to end of line - `d$`
- To move the cursor to particular line number - `:n` where n can be any number
- To copy (yank) multiple characters based on selection
	- Go to visual mode by `v`
	- Move your cursor to select the characters/lines
	- To copy the selected lines `y`. This will only copy to VIM's clipboard.
- To delete multiple characters (or lines) based on selection
	- Go to visual mode by `v`
	- Move your cursor to select the characters/lines
	- To delete the selected lines `d`
- To paste the copied (yanked) text - `p`
- To go to the end of line - `$`
- To go to the beginning of line - `^`
- To move one word at a time - `w`
- To delete a single character - `x`

## NERDTree Plugin

- To cycle through the different panes - `Ctrl + w + w`