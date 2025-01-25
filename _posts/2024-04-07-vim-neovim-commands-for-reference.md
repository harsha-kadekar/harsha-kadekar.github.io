---
category: Technical
date: 2024-04-07
layout: post
title: VIM/NVIM Commands for Reference
updated: 2024-11-07
---

In this post, I will capture all the common commands I use often so that I do not have to do google search every-time I want to type something in NVIM


## General Commands

In general, format is `<count><action><scope><object>`

- To delete a line -  `dd`
- To delete a word - `dw`
- To delete from cursor to end of line - `d$` or `D`
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
- To go to the corresponding closing bracket (you need cursor to be on top of opening bracket) - `%`
- To delete all the characters from the current cursor position till the next occureance of character - `dtx` where `x` is the character you wish like `dt"`. So delete till you find `"`.
- To remove everything between the quotes and place cursor after quotes - `ciq`
- To delete all the elements between brackets - `dab`
- To copy the current word your cursor is in - `yiw`
- To select all the lines with current indentation - `vii`
- to select all the elements around bracket - `vab`

## NERDTree Plugin

- To cycle through the different panes - `Ctrl + w + w` 

## LazyVim 
- To Open file explorer - `space + e`
- To move to the left tab - `Shift + H`
- To move to the right tab - `Shift + L`
- To cycle through different panes - `ctrl + w + w`
- To close an open tab - `space B D`
- To close all the open tab but the current one - `space B O`
- To create a new directory - navigate to the folder under which you want to create the directory and then - `A`
- To create a new file - navigate to the folder under which you want to create the file and then - `a`