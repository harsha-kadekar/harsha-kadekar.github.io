---
category: Technology
date: 2022-05-13
layout: post
title: My Personal and Development Configuration
updated: 2024-03-24
---

In this post, I would like to explain about development configurations and development tools I use in my personal system. I have a laptop with dual partition. My primary partition is [Ubuntu Operating System](https://ubuntu.com) and the secondary partition is [Windows 11 Operating System](https://www.microsoft.com/en-us/windows?r=1). My early exposure to computer started via Windows and continued in Windows for a long-time. I switched to Linux once I joined Amazon. At my workplace, I use Mac and Linux. Almost all the things I use in Mac are Linux compatible software.
{: style="text-align: justify;"}

Here are the few tools I use in personal system.
- [Alacritty](https://alacritty.org): This is a terminal emulator. The reason I chose this because it is cross platform. Same terminal can be used in Mac OS and Linux. Mac OS has [iTerm2](https://iterm2.com) which has better features but it is not available in Linux. Hence, as of now I stick to alacritty. Another plus point of alacritty, is its ability to configure. My dot file for alacritty can be found [here](https://github.com/harsha-kadekar/dotfiles/blob/main/alacritty.yml)
- [OhMyZsh](https://ohmyz.sh/): My default shell is `zsh`. On top of that, I use `OhMyZsh`. *OhMyZsh* provides a set of functions and plugins for the terminal which makes it easy to work with your shell. *OhMyZsh* has a great set of plug-ins. My dotfile for zsh can be found [here](https://github.com/harsha-kadekar/dotfiles/blob/main/zshrc). Among the ohmyzsh plugins, I particularly use following -
	- [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting): This helps in highlighting the syntax of the commands in zsh. Pretty useful in catching some small errors. It also makes your shell pleasing.
	- [zsh-autosuggesions](https://github.com/zsh-users/zsh-autosuggestions): This suggests the commands as you type in based on the history. Quite useful when you are using repeated commands.
- [TMUX](https://github.com/tmux/tmux/wiki): This is a terminal multiplexer. In a single window of terminal, we can work on multiple things by dividing the window. It also maintains our environments as session. We can configure it with various plugins. You can find my T-Mux dot file [here](https://github.com/harsha-kadekar/dotfiles/blob/main/tmux.conf). Here are the plug-ins I use -
	- [Tmux plug-in manager](https://github.com/tmux-plugins/tpm): The plug-ins in T-Mux can be managed by different plug-in manager. I personally use this. I have not used any other managers and this has never caused any issues till date.
	- [Tmux Sensible](https://github.com/tmux-plugins/tmux-sensible): This plug-in helps us to add some settings like key bindings.
	- [tmux-battery](https://github.com/tmux-plugins/tmux-battery): This plug-in helps in displaying the current laptop battery percentage in the T-Mux window.
	- [tmux-cpu](https://github.com/tmux-plugins/tmux-cpu): This plug-in helps in displaying the current CPU usage and RAM usage.
- [NeoVim](https://neovim.io): This is a terminal text editor. It is extensible with lot of plug-ins. This will be my go to text editor for small changes to the file or writing small programs. [Here](https://github.com/harsha-kadekar/dotfiles/blob/main/init.vim) is my dot file for neovim. Some of the plug-ins I use-
	- [vim-plug](https://github.com/junegunn/vim-plug): Vim Plug is my plugin manager for neovim. I have not used other plugin managers and this has not caused any issues so all good.
	- [NERDTree](https://github.com/preservim/nerdtree): This provides the file system explorer within Vim editor. This is useful when you are working on a package and you need to edit multiple files.
	- [vim-airline](https://github.com/vim-airline/vim-airline): This provides an intitutive status bar to VIM windows.
	- [vim-gitgutter](https://github.com/airblade/vim-gitgutter): When a file is getting edited, this will track the git changes and mark them for easy identification.
	- [vim-sensible](https://github.com/tpope/vim-sensible): These helps to set some of the common configurations in the vim.
- [Microsoft Visual Code](https://code.visualstudio.com): This is the editor I generally use for small projects from Java, Python, Angular, Ruby, Rust, you name it. The use-case of this fits between NeoVim and full fledged IDEs.
- [IntelliJ Idea Community Edition](https://www.jetbrains.com/idea/): This is my go to IDE for Java related projects.
- [IntelliJ Pycharm](https://www.jetbrains.com/pycharm/): This is my go to IDE for python related projects.
- [Obsidian](https://obsidian.md): This is my note taking as well as journaling app. It is high customisation abilities and all the data is under my control (I store it in my private Github repo). 
- [Vivaldi](https://vivaldi.com): This is my default browser.
- [FireFox](https://www.mozilla.org/en-US/firefox/new/): FireFox is my backup browser.
- [Ulaa](https://ulaa.com): This is also my backup browser. I flip between Firefox and Ulaa.
- [Zoho Notebook](https://www.zoho.com/notebook/): This is my mobile note taking app.
- [KeyPass](https://keepass.info): This is my password storage tool.

The dot file configurations are not my own creation, rather I have taken from multiple places and tried to fit into something what works for me. If you use any good tools or configurations do let me know, so that I can try it.
{: style="text-align: justify;"}