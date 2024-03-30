---
category: Technical
date: 2024-02-15
layout: post
title: Obsidian To Github Pages Script
updated: 2024-02-15
---

## Overview
I use [Github Pages](https://pages.github.com) to publish my blog ([harsha-kadekar.github.io](https://harsha-kadekar.github.io)). The source code of the blog is stored in the [Github Repository](https://github.com/harsha-kadekar/harsha-kadekar.github.io). As part of github pages, Github will automatically build it from my github repository and publish with a DNS. The framework used is [Jekyll](https://jekyllrb.com).  It converts the markdown files into static websites. On top of that we can apply some theme to our blog. So, it has minimal `javascript` and `css` styling components. Each post of the blog is a markdown file in your repository.
{: style="text-align: justify;"}
## Why I created this script?
Till recently, I used Microsoft Visual Studio Code as the editor to modify the github repository of the blog. Given that most of the editing I will be doing for the blog is just writing markdown files, I was kind of using Visual Studio Code as a markdown editor. 
{: style="text-align: justify;"}

I use [Obsidian](https://obsidian.md) as the note taking as well as journaling application. It puts everything as markdown files and make writing markdown files fun. Even at work I use `Obsidian` for note taking. 
{: style="text-align: justify;"}

At work, one of my colleague came up with a script to publish notes written in Obsidian to internal wiki. The internal wiki is kind of a place where you can put information that can be accessible through out the company.  This made me think does similar feature exists for my personal blog. That is, I will write notes in `Obsidian` and some plugin/external script can be used to migrate those notes to posts of my blog. I know that Obsidian has [Obsidian Publish](https://obsidian.md/publish) plug-in. That is not free and I also wanted something to work with my existing blog which is Github page based. I came across this blog - [How I publish my zettelkasten](https://person-al.github.io/%F0%9F%8C%B3/2022/05/08/how-i-publish-my-zettelkasten.html), which explained how they use `Obsidian` and publish to Github pages repository.  They used [Obdye](https://github.com/notkmhn/obyde) to do the conversion for Obsidian notes to Github Pages post.  Based on this, I have started moving all of the old posts in my blog to Obsidian. I also wrote a wrapper script - [ObsidianToGithubPages](https://github.com/harsha-kadekar/ObsidianToGithubPages/blob/main/obsidian_to_githubpages.py) around `Obdye` to execute them to convert it back to posts.  Also for some reason, `Obdye` does not support `pages` layout. Hence, I wrote a custom script on top of the `Obdye` to do all the post work + `Obdye`. Lets understand about the script and how to use it.
{: style="text-align: justify;"}
## ObsidianToGithubPages
### Prerequisite
- This is a python based script and hence in-order to execute this script, we need python to be installed in the system.  
- The script is a wrapper script around the [Obdye](https://github.com/notkmhn/obyde). Hence, it expects Obdye is already installed.
	- Here is the installation instructions from Obdye - [installation instructions](https://github.com/notkmhn/obyde?tab=readme-ov-file#installation)
- All your notes which needs to be published need to reside under a single folder within your Obsidian vault.

### Assumptions
- It assumes that in your github page repository, all the posts in a directory named `_posts`.
- It assumes that all the assets related to your posts will reside in folder `assets` under the github page repository
- Under the Obsidian vault folder, any notes present under `drafts` will be ignored
- Under the Obsidian vault folder, all the assets related to the notes are present in the `assets` folder

### How to use
The script `obsidian_to_githubpages.py` can be executed with following command - 
```shell
./obsidian_to_githubpages.py --obsidian_local_vault <local path of the obsidian vault> --github_pages_repo_local <local repository path of github pages>
```

Example, lets say your local Obsidian vault stays at location `/home/myalias/workspace/mypersonalvault` and the local github pages repo exists at location `/home/myalias/workspace/mypages-blog`

```shell
./obsidian_to_githubpages.py --obsidian_local_vault "/home/myalias/workspace/mypersonalvault" --github_pages_repo_local "/home/myalias/workspace/mypages-blog"
```

Here it makes an assumption that, all the notes present in the vault under folder `Blog` will be considered for the migration. If we want to use a different folder use following command
{: style="text-align: justify;"}

```shell
./obsidian_to_githubpages.py --obsidian_local_vault <local path of the obsidian vault> --github_pages_repo_local <local repository path of github pages> --blog_folder <blog folder name>
```

Example:

```shell
./obsidian_to_githubpages.py --obsidian_local_vault "/home/myalias/workspace/mypersonalvault" --github_pages_repo_local "/home/myalias/workspace/mypages-blog" --blog_folder ToPublish
```

### How it works?
Internally, it will create a config file to be used by the `Obyde`. Example, if the input was provided with this - 
{: style="text-align: justify;"}

```shell
./obsidian_to_githubpages.py --obsidian_local_vault "/home/myalias/workspace/mypersonalvault" --github_pages_repo_local "/home/myalias/workspace/mypages-blog" --blog_folder ToPublish
```

It will create the config file as 

```yaml
vault:
  path: /home/myalias/workspace/mypersonalvault/ToPublish
  asset_path: /home/myalias/workspace/mypersonalvault/ToPublish/assets
  excluded_subdirectories:
  - drafts
output:
  post_output_path: /home/myalias/workspace/mypages-blog/_posts
  asset_output_path: /home/myalias/workspace/mypages-blog/assets
  relative_asset_path_prefix: '{{ site.blog_assets_location }}'
  post_link_jekyll: jekyll
```

Once this config file is created, it will call the `obdye` with this config file as the argument.
`Obyde` will convert all the markdown files under the folder `/home/myalias/workspace/mypersonalvault/ToPublish` to posts. It expects that each file has properties with `layout` and `date`. Once `obdye` conversion is completed, the script will go through all the generated posts in the github page repo and if it finds any `layout` with value as `page` it will move them to parent directory of the `_posts` and also remove the prefixed date from the file names. Thats it! your local repo of the blog is read to be consumed. Check it inn to see the updates in your blog.
{: style="text-align: justify;"}