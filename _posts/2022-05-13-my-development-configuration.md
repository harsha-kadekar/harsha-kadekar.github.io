---
category: Technical
date: 2022-05-13
layout: post
title: My Personal and Development Configuration
updated: 2026-02-14
---

In this post, I would like to explain about tools I use for my development in my personal system. The detailed step of personal laptop configuration is found in the post - [My Personal Laptop Setup]({% post_url 2026-02-14-my-personal-laptop-setup %}).

I use [Ubuntu Operating System](https://ubuntu.com)  at home. 
{: style="text-align: justify;"}

Here are the tools I use in personal system (as of now).
- [Obsidian](https://obsidian.md): This is my note taking as well as journaling app. It is high customisation abilities and all the data is under my control (I store it in my private Github repo). 
- [Ghostty](https://ghostty.org) - This is a terminal emulator. The reason I chose this because it is cross platform. I can use same terminal in Mac OS (at work) and in Linux (at home). It needs no configuration as it comes with loaded features. I have a config for style purpose like font and theme. Earlier, I used to use [Alacritty](https://alacritty.org).  My ghostty config can be found in my [dotfile repo](https://github.com/harsha-kadekar/dotfiles/blob/main/ghostty_config).
- [OhMyZsh](https://ohmyz.sh/): My default shell is `zsh`. On top of that, I use `OhMyZsh`. *OhMyZsh* provides a set of functions and plugins for the terminal which makes it easy to work with your shell. *OhMyZsh* has a great set of plug-ins. My dotfile for zsh can be found [here](https://github.com/harsha-kadekar/dotfiles/blob/main/zshrc). Among the ohmyzsh plugins, I particularly use following -
	- [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting): This helps in highlighting the syntax of the commands in zsh. Pretty useful in catching some small errors. It also makes your shell pleasing.
	- [zsh-autosuggesions](https://github.com/zsh-users/zsh-autosuggestions): This suggests the commands as you type in based on the history. Quite useful when you are using repeated commands.
- [Zellij](https://zellij.dev): This is a terminal multiplexer. In a single window of terminals, we can work on multiple things by dividing the window or adding more terminal tabs. We can even configure this. It does not need any extra configurations as it comes with tone of features. But, I have a small config change to serialize the sessions. The config can be found in the [dotfile repo](https://github.com/harsha-kadekar/dotfiles/blob/main/zellij_config.kdl).  Before I started using zellij, I used to use [TMUX](https://github.com/tmux/tmux/wiki).
- [Helix](https://helix-editor.com): This is my default terminal editor. It also comes with tones of features packed and does not need any extra configuration to start working with. If it is single file changes or few file changes then I use this editor instead of going for a GUI editor.
	- I still keep [NeoVim](https://neovim.io) with following config  [here](https://github.com/harsha-kadekar/dotfiles/blob/main/init.vim) just as a back-up. Some of the plug-ins I use in neovim are - 
		- [vim-plug](https://github.com/junegunn/vim-plug): Vim Plug is my plugin manager for neovim. I have not used other plugin managers and this has not caused any issues so all good.
		- [NERDTree](https://github.com/preservim/nerdtree): This provides the file system explorer within Vim editor. This is useful when you are working on a package and you need to edit multiple files.
		- [vim-airline](https://github.com/vim-airline/vim-airline): This provides an intitutive status bar to VIM windows.
		- [vim-gitgutter](https://github.com/airblade/vim-gitgutter): When a file is getting edited, this will track the git changes and mark them for easy identification.
		- [vim-sensible](https://github.com/tpope/vim-sensible): These helps to set some of the common configurations in the vim.
- [Claude Code](https://code.claude.com/docs/en/overview): This is my LLM assistant. 
- [Zed](https://zed.dev): This is my go to editor for all the small programming projects.
- [IntelliJ Idea Community Edition](https://www.jetbrains.com/idea/): This is my go to IDE for Java related projects.
- [IntelliJ Pycharm](https://www.jetbrains.com/pycharm/): This is my go to IDE for python related projects.
- [Vivaldi](https://vivaldi.com): This is my default browser.
- [Zoho Notebook](https://www.zoho.com/notebook/): This is my mobile note taking app.
- [Instapaper](https://www.instapaper.com): I use this for mobile reading of bookmarked articles. This helps with offline reading.
- [Arattai](https://www.arattai.in): I prefer this chatting app but most of my network is still in [whatsapp](https://www.whatsapp.com)
- [KeyPass](https://keepass.info): This is my password storage tool. I use this version [KeePassXC](https://keepassxc.org/)
- [Spotify](https://open.spotify.com): This is my music playlist app.
- [Fusion RSS Reader](https://github.com/0x2E/fusion): To collect all the feeds for blogs I follow. 

The dot file configurations are not my own creation, rather I have taken from multiple places and tried to fit into something what works for me. If you use any good tools or configurations do let me know, so that I can try it.
{: style="text-align: justify;"}