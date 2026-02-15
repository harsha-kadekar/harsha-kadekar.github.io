---
category: Technical
date: 2026-02-14
layout: post
title: My Personal Laptop Setup
updated: 2026-02-14
---

This post describes how I setup my personal laptop. The use my personal laptop for few things at home
- Personal Home Management Tool - Keeping track of tasks, accounting, preparing documents, investigating about various chores, etc.
- Personal Home Entertainment System - We do not have a separate T.V. at home. Any entertainment we want to view is via this personal compute and a big monitor.
- Development Machine - Used for our personal tech projects. Both me and my wife has our own login and we code and build stuff. 

## OS installation
I use [Ubuntu](https://ubuntu.com/desktop) as the operating system. During the installation go for advanced option in-order to select the preferred partition. Here is the partitions I use in  Ubuntu.
- 128 Gb for `root(/)`
- 1 Gb for `/boot`
- 32 Gb for `swap` (equal to the RAM size - can be less if need be)
- Rest is reserved for `/home` 

## Software Installations

- Register the OS installation in the UbuntuPro
- Install [Vivaldi](https://vivaldi.com) web browser
	- Install it via App Center.
	- Make Vivaldi default browser - Settings > Apps > Default Apps > Web (set to Vivaldi)
	- Login to Vivaldi - in-order to carry forward the configurations, setting, recover tabs if needed
	- I use [Crystal Blue](https://themes.vivaldi.net/themes/2zmvzjmBv6g) as light theme
	- I use [Western Ghats](https://themes.vivaldi.net/themes/40y7Q8ObJXx) as dark theme
	- Install following extensions
		- [Obsidian Web Clipper](https://obsidian.md/clipper)
		- [Instapaper](https://chromewebstore.google.com/detail/instapaper/ldjkgaaoikpmhmkelcgkgacicjfbofhh?hl=en)
		- [Zoho Notebook](https://help.zoho.com/portal/en/kb/zoho-sprints/marketplace/zoho-apps/articles/zoho-notebook-extension)
- Install [ghostty](https://ghostty.org/docs/install/binary#linux-(official)) terminal
	- Install it via App Center
	- Copy the [config](https://github.com/harsha-kadekar/dotfiles/blob/main/ghostty_config) and place it in the directory as mentioned in [README](https://github.com/harsha-kadekar/dotfiles/blob/main/README.md) file.
		- Install the fonts as mentioned in the README file.
- Set `zsh` as the default shell
	- Install `zsh` shell if it is not already installed. Here is a [reference for steps](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH#install-and-set-up-zsh-as-default)
		- Verify if present `which zsh`
		- `echo $0` should output `/usr/bin/zsh`
		- Install zsh `sudo apt install zsh`
		- change to zsh shell - `chsh -s $(which zsh)`
- Install build essentials
	- Essentials for other packages - `sudo apt install build-essential libssl-dev libreadline-dev libyaml-dev libffi-dev`
	- Install Rust Language - https://rust-lang.org/tools/install/
	- Install Go Language from the App Center
	- Install [Mise](https://mise.jdx.dev)(mise-en-place) from App Center to manage - node, npm, node, python and ruby
		- add `eval "$(mise activate zsh)"` to `~/zshrc` file if not added automatically
		- Install node - `mise use -g node`
		- Install npm - `mise use -g npm`
		- Install pnpm - `mise use -g pnpm`
		- Install ruby - `mise use -g ruby`
		- Install python  -`mise use -g python`
	- Install `curl` - `sudo apt-get install curl`. Do not use snap for this as it has some issues for later zellij and rust installation. 
- Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and configure Github
	- Git Installation - `sudo apt install git-all`
	- Setup up git global parameters
		- `git config --global user.email "harsha.kadekar@gmail.com"`
		- `git config --global user.name "Harsha Kadekar"`
	- Configure Github to operated with the current laptop ssh keys.
		- [Generate new ssh keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) - `ssh-keygen -t ed25519 -C "harsha.kadekar@gmail.com"`
		- [Add the key to the Github profile](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
- Install Terminal enhancers
	- Install [oh-my-zsh](https://ohmyz.sh/#install)
	- Install plug-ins of oh-my-zsh
		- [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh) install via oh-my-zsh (git cloning)
		- [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md#oh-my-zsh) install via oh-my-zsh (git cloning)
	- Install [Zellij](https://zellij.dev)
		- Install via cargo - `cargo install --locked zellij`
		- Copy the configuration as mentioned in [README](https://github.com/harsha-kadekar/dotfiles/blob/main/README.md) file.
		- Add `alias zellij="zellij -l welcome"` to `~/.zshrc` file
	- Install [htop](https://htop.dev/downloads.html) - enhanced top
		- Install via App Center.
	- Install [Yazi](https://yazi-rs.github.io) - terminal file manager
		- Install via App Center.
- Install editors and IDE
	- Install [helix](https://helix-editor.com) terminal editor
		- Install via App Center
	- Install [NeoVim](https://neovim.io)
		- Install via App Center
		- Install [vim-plug](https://github.com/junegunn/vim-plug) plugin-manager 
		- Copy the nvim config as mentioned in the [README](https://github.com/harsha-kadekar/dotfiles/blob/main/README.md) file.
		- Install plug-ins by opening `nvim` and run command `:PlugInstall`
	- Install [Zed](https://zed.dev/download) editor
		- Add `export PATH=$HOME/.local/bin:$PATH` to `~/.zshrc` file
	- Install Jetbrains IDE
		- Install [toolbox](https://www.jetbrains.com/toolbox-app/) via `.tar.gz` file. Extract and run the script (follow readme inside).
		- Install following IDEs
			- Idea
			- RustRover
			- Pycharm
			- Getway
- Create a folder `workspace` folder
	- `mkdir $HOME/workspace`
- Install [Obsidian](https://obsidian.md)
	- Install by [downloading the `.deb`](https://obsidian.md/download) file (do not install via snap/App center - it has issues with the Obsidian Web Clipper browser extension)
	- Clone the Obsidian Vault from Github Repository at location `$HOME/workspace`
	- Setup Obsidian as mentioned in this blog post (ToDo://add obsidian setup post link)
- Install [KeePassXC](https://keepassxc.org/download/#linux)
	- Install via App Center
- Install [Claude Code](https://code.claude.com/docs/en/overview)
	- Login
	- Set-up claude (ToDo:// add personal claude code setup post link)
- Pull In [Fusion Rss Feed Reader](https://github.com/0x2E/fusion)
	- `./scripts.sh build`
	- Copy over the `fusion` db and `env` config file from the cloud drive to `build` folder
- Install [Spotify](https://open.spotify.com/download)
	- Install via App Center
- Install [Arattai](https://www.arattai.in/download.html)
- Add ಕನ್ನಡ (Kannada) Language Support in Ubuntu
	- In `Language Support` add ಕನ್ನಡ
	- In Settings > Keyboard > Input Sources add `Kannada (KaGaPa, phonetic)`
- Some Repositories I use often
	- My blog - https://github.com/harsha-kadekar/harsha-kadekar.github.io
		- Git clone the repository at location `$HOME/workspace`
		- In the repository folder, execute `bundle install`
		- Add this alias `alias dry-run-blog="bundle exec jekyll serve"` in `~/.zshrc` file.
		- In the repository folder, execute `dry-run-blog` to verify the blog gets hosted in `localhost`
	- Obsidian To Github Pages Converter - https://github.com/harsha-kadekar/ObsidianToGithubPages
		- Git clone the repository at location `$HOME/workspace`
		- Install dependencies as mentioned in the [README](https://github.com/harsha-kadekar/ObsidianToGithubPages/blob/main/README.md) file
		- Add this alias `alias transform-to-blog='/home/harsha/workspace/ObsidianToGithubPages/obsidian_to_githubpages.py --obsidian_local_vault "/home/harsha/workspace/pusthaka" --github_pages_repo_local "/home/harsha/workspace/harsha-kadekar.github.io" --blog_folder "Blog"'` in `~/.zshrc` file
		- Execute `tranform-to-blog` command to verify it is working
- Install Secondary Softwares (Optional)
	- Install [alacritty](https://alacritty.org) terminal
		- Install via App Center
	- Install [ullaa](https://ulaa.com) web browser

## Configure Wife User

We want to have separate users but also a shared folder to exchange date between us. Claude helped me to come up with these steps

- Create user `sudo adduser anu`
- Add `anu` to sudo group `sudo usermod -aG sudo harsha`
	- Log In to `anu` user and change to `zsh` shell
	- Log Off & Log In to `harsha` user
- Create `kadekar` group - `sudo groupadd kadekar`
- Add users to the `kadekar` group
	- `sudo usermod -aG kadekar harsha`
	- `sudo usermod -aG kadekar anu`
- Create a shared folder in `/home`
	- `sudo mkdir /home/shared`
	- `sudo chown root:kadekar /home/shared`
	- `sudo chmod 2770 /home/shared`
- Set `unmask` in shell profiles to make sure both of us create files  having permission for `kadekar` group.
	- `echo "umask 002" | sudo tee -a /home/harsha/.zshrc`
	- `echo "umask 002" | sudo tee -a /home/anu/.zshrc`
- Create symlinks for the shared folder within our home directories
	- `ln -s /home/shared ~/shared`
	- `sudo -u anu ln -s /home/shared /home/anu/shared`