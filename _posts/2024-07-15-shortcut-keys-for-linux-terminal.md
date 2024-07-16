---
category: Technical
date: 2024-07-15
layout: post
title: Shortcut Keys for Linux Terminal
updated: 2024-07-15
---

I use Linux terminal a lot. During the day to day usage of terminal, we have to move around the cursor a lot. Given that terminal is a command line interface and not a graphical user interface, we cannot just move our mouse and click to the point where we want the cursor. So, here are some of the shortcut keys to move around the terminal faster.

- `up arrow` -> to go to the previous executed command
- `down arrow` -> to go to the next executed command
- `left arrow` -> to move one position to the left
- `right arrow` -> to move one position to the right
- `ctrl + a` -> to move the cursor to the beginning of the line/row
- `ctrl + e` -> to move the cursor to the end of the line/row
- `ctrl + w` -> to delete the current word on which cursor exists
- `alt + f` -> to move cursor to the next word
- `alt + b` -> to move cursor to the previous word
- `ctrl + k` -> to delete from cursor to the end of line
- `ctrl + u` -> to delete from cursor to the beginning of line (if you are using zsh then you need to add `bindkey \^U backward-kill-line` to `.zshrc` file)
- `ctrl + y` -> to yank/paste the copied/cut contents at the cursor position
- `ctrl + c` -> to stop the feed/kill the existing process
- `ctrl + d` -> to exit the terminal