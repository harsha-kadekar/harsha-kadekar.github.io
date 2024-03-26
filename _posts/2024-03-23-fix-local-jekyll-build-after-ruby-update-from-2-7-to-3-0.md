---
category: Technology
date: 2024-03-23
layout: post
title: Fix Local Jekyll build after ruby update from 2.7 to 3.0
updated: 2024-03-23
---

## Problem Statement

I use [Github Pages](https://pages.github.com) to host my blog. The Github Pages use [Jekyll](https://jekyllrb.com)to generate the blog. Jekyll is a static site generator, given the markdown files it will convert them into html files. One of the prerequisite for Jekyll is [Ruby](https://www.ruby-lang.org/en/).   

Recently, local build of my Jekyll generated blog started failing with error -  

```
  harsha-kadekar.github.io git:(master) ✗ bundle exec jekyll serve
/usr/bin/env: ‘ruby2.7’: No such file or directory
```


## Fix

- Re-install `bundle` and `jekyll` using command `gem install jekyll bundler`
- Add `webrick` using command `bundle add webrick`
- Fix `pathutil` by adding this in the Gemfile `gem "pathutil", github: "sdogruyol/pathutil", ref: '6ab144a7706c2bc5fa0dfdfa498e94ff66e944c6'`
- If you use theme `no-style-please` , then make sure you have installed `jekyll 3.9` by using command `gem install jekyll -v 3.9.0`
- Re-install `ffi` using `gem install ffi`

## Debug

My initial thought was  `ruby` runtime might have got uninstalled in my laptop. To verify this hypothesis, ran this command -  

```
  harsha-kadekar.github.io git:(master) ✗ ruby -v
ruby 3.0.2p107 (2021-07-07 revision 0db68f0233) [x86_64-linux-gnu]
```

So `ruby` still exists but the version is `3.0` instead of `2.7`. So, now the problem statement got updated in my mind -  `due to update of ruby from version 2.7 to version 3.0 in my laptop, jekyll execution in the system started failing`. I thought the issue was in `bundle` itself, so as a first step, verified that `bundle` loading as expected.

```
➜  harsha-kadekar.github.io git:(master) ✗ bundle -v
/usr/bin/env: ‘ruby2.7’: No such file or directory
```

As a fix, tried to re-install `bundler` and `jekyll`.

```
➜  harsha-kadekar.github.io git:(master) ✗ gem install jekyll bundler

Fetching jekyll-4.3.3.gem
Fetching webrick-1.8.1.gem
Successfully installed webrick-1.8.1
Successfully installed jekyll-4.3.3
Parsing documentation for webrick-1.8.1
Installing ri documentation for webrick-1.8.1
Parsing documentation for jekyll-4.3.3
Installing ri documentation for jekyll-4.3.3
Done installing documentation for webrick, jekyll after 2 seconds
Fetching bundler-2.5.7.gem
Successfully installed bundler-2.5.7
Parsing documentation for bundler-2.5.7
Installing ri documentation for bundler-2.5.7
Done installing documentation for bundler after 0 seconds
3 gems installed
```

```
➜  ~ bundle -v
Bundler version 2.5.7
```

Once this was validated, tried to re-run jekyll static site generator. It failed again with a different error - 

```
  harsha-kadekar.github.io git:(master) ✗ bundle exec jekyll serve
Configuration file: /home/harsha/workspace/harsha-kadekar.github.io/_config.yml
            Source: /home/harsha/workspace/harsha-kadekar.github.io
       Destination: /home/harsha/workspace/harsha-kadekar.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
       Jekyll Feed: Generating feed for posts
                    done in 0.484 seconds.
jekyll 3.9.0 | Error:  no implicit conversion of Hash into Integer
/home/harsha/gems/gems/pathutil-0.16.2/lib/pathutil.rb:502:in `read': no implicit conversion of Hash into Integer (TypeError)
        from /home/harsha/gems/gems/pathutil-0.16.2/lib/pathutil.rb:502:in `read'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/utils/platforms.rb:75:in `proc_version'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/utils/platforms.rb:40:in `bash_on_windows?'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/build.rb:77:in `watch'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/build.rb:43:in `process'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/serve.rb:93:in `block in start'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/serve.rb:93:in `each'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/serve.rb:93:in `start'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/serve.rb:75:in `block (2 levels) in init_with_program'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary/command.rb:220:in `block in execute'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary/command.rb:220:in `each'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary/command.rb:220:in `execute'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary/program.rb:42:in `go'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary.rb:19:in `program'
        from /home/harsha/gems/gems/jekyll-3.9.0/exe/jekyll:15:in `<top (required)>'
        from /home/harsha/gems/bin/jekyll:25:in `load'
        from /home/harsha/gems/bin/jekyll:25:in `<top (required)>'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/cli/exec.rb:58:in `load'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/cli/exec.rb:58:in `kernel_load'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/cli/exec.rb:23:in `run'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/cli.rb:483:in `exec'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/vendor/thor/lib/thor/command.rb:27:in `run'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/vendor/thor/lib/thor/invocation.rb:127:in `invoke_command'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/vendor/thor/lib/thor.rb:392:in `dispatch'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/cli.rb:31:in `dispatch'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/vendor/thor/lib/thor/base.rb:485:in `start'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/cli.rb:25:in `start'
        from /home/harsha/gems/gems/bundler-2.3.13/exe/bundle:48:in `block in <top (required)>'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/friendly_errors.rb:103:in `with_friendly_errors'
        from /home/harsha/gems/gems/bundler-2.3.13/exe/bundle:36:in `<top (required)>'
        from /home/harsha/gems/bin/bundle:25:in `load'
        from /home/harsha/gems/bin/bundle:25:in `<main>'
```

I looked around the web and found these references. Even in  `jekyll` documentation, it asked to add `webrick` if using `ruby 3.0`
- [github pages - testing your github pages site locally with jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll#building-your-site-locally)
- [jekyll docs](https://jekyllrb.com/docs/)

```
  harsha-kadekar.github.io git:(master) ✗ bundle add webrick
```

Even after adding `webrick`, error persisted.

```
  harsha-kadekar.github.io git:(master) ✗ bundle exec jekyll serve
Configuration file: /home/harsha/workspace/harsha-kadekar.github.io/_config.yml
            Source: /home/harsha/workspace/harsha-kadekar.github.io
       Destination: /home/harsha/workspace/harsha-kadekar.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
       Jekyll Feed: Generating feed for posts
                    done in 0.373 seconds.
jekyll 3.9.0 | Error:  no implicit conversion of Hash into Integer
/home/harsha/gems/gems/pathutil-0.16.2/lib/pathutil.rb:502:in `read': no implicit conversion of Hash into Integer (TypeError)
        from /home/harsha/gems/gems/pathutil-0.16.2/lib/pathutil.rb:502:in `read'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/utils/platforms.rb:75:in `proc_version'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/utils/platforms.rb:40:in `bash_on_windows?'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/build.rb:77:in `watch'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/build.rb:43:in `process'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/serve.rb:93:in `block in start'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/serve.rb:93:in `each'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/serve.rb:93:in `start'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/serve.rb:75:in `block (2 levels) in init_with_program'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary/command.rb:220:in `block in execute'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary/command.rb:220:in `each'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary/command.rb:220:in `execute'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary/program.rb:42:in `go'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary.rb:19:in `program'
        from /home/harsha/gems/gems/jekyll-3.9.0/exe/jekyll:15:in `<top (required)>'
        from /home/harsha/gems/bin/jekyll:25:in `load'
        from /home/harsha/gems/bin/jekyll:25:in `<top (required)>'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/cli/exec.rb:58:in `load'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/cli/exec.rb:58:in `kernel_load'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/cli/exec.rb:23:in `run'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/cli.rb:483:in `exec'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/vendor/thor/lib/thor/command.rb:27:in `run'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/vendor/thor/lib/thor/invocation.rb:127:in `invoke_command'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/vendor/thor/lib/thor.rb:392:in `dispatch'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/cli.rb:31:in `dispatch'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/vendor/thor/lib/thor/base.rb:485:in `start'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/cli.rb:25:in `start'
        from /home/harsha/gems/gems/bundler-2.3.13/exe/bundle:48:in `block in <top (required)>'
        from /home/harsha/gems/gems/bundler-2.3.13/lib/bundler/friendly_errors.rb:103:in `with_friendly_errors'
        from /home/harsha/gems/gems/bundler-2.3.13/exe/bundle:36:in `<top (required)>'
        from /home/harsha/gems/bin/bundle:25:in `load'
        from /home/harsha/gems/bin/bundle:25:in `<main>'
```

Again searched for this specific error, and found some references - 
- [https://bbs.archlinux.org/viewtopic.php?id=265534](https://bbs.archlinux.org/viewtopic.php?id=265534)
- [https://talk.jekyllrb.com/t/error-no-implicit-conversion-of-hash-into-integer/5890/10](https://talk.jekyllrb.com/t/error-no-implicit-conversion-of-hash-into-integer/5890/10)
- [https://stackoverflow.com/questions/66113639/jekyll-serve-throws-no-implicit-conversion-of-hash-into-integer-error](https://stackoverflow.com/questions/66113639/jekyll-serve-throws-no-implicit-conversion-of-hash-into-integer-error)
All pointing to the incompatible `pathutil`. Then, based on the following suggestions - 
- [https://stackoverflow.com/a/77679717](https://stackoverflow.com/a/77679717)
- [https://github.com/envygeeks/pathutil/pull/5/commits/3451a10c362fc867b20c7e471a551b31c40a0246/](https://github.com/envygeeks/pathutil/pull/5/commits/3451a10c362fc867b20c7e471a551b31c40a0246/)

updated the gemfile of my blog to be something like this - 

```
# frozen_string_literal: true

source "https://rubygems.org"

gem "kramdown-parser-gfm"

gemspec
gem "webrick", "~> 1.8"
gem "pathutil", github: "sdogruyol/pathutil", ref: '6ab144a7706c2bc5fa0dfdfa498e94ff66e944c6'
```

```
➜  harsha-kadekar.github.io git:(master) ✗ bundle install
```

Now a new error started, when I retried - 

```
➜  harsha-kadekar.github.io git:(master) ✗ bundle exec jekyll serve --trace
Ignoring commonmarker-0.17.13 because its extensions are not built. Try: gem pristine commonmarker --version 0.17.13
Ignoring ffi-1.15.5 because its extensions are not built. Try: gem pristine ffi --version 1.15.5
Ignoring ffi-1.15.1 because its extensions are not built. Try: gem pristine ffi --version 1.15.1
Ignoring http_parser.rb-0.6.0 because its extensions are not built. Try: gem pristine http_parser.rb --version 0.6.0
Ignoring json-2.5.1 because its extensions are not built. Try: gem pristine json --version 2.5.1
Ignoring racc-1.5.2 because its extensions are not built. Try: gem pristine racc --version 1.5.2
Ignoring unf_ext-0.0.7.7 because its extensions are not built. Try: gem pristine unf_ext --version 0.0.7.7
Configuration file: /home/harsha/workspace/harsha-kadekar.github.io/_config.yml
            Source: /home/harsha/workspace/harsha-kadekar.github.io
       Destination: /home/harsha/workspace/harsha-kadekar.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
       Jekyll Feed: Generating feed for posts
                    done in 0.372 seconds.
bundler: failed to load command: jekyll (/home/harsha/gems/bin/jekyll)
/home/harsha/gems/gems/ffi-1.16.3/lib/ffi.rb:5:in `require': incompatible library version - /home/harsha/gems/gems/ffi-1.16.3/lib/ffi_c.so (LoadError)
        from /home/harsha/gems/gems/ffi-1.16.3/lib/ffi.rb:5:in `rescue in <top (required)>'
        from /home/harsha/gems/gems/ffi-1.16.3/lib/ffi.rb:2:in `<top (required)>'
        from /home/harsha/gems/gems/rb-inotify-0.10.1/lib/rb-inotify/native.rb:1:in `require'
        from /home/harsha/gems/gems/rb-inotify-0.10.1/lib/rb-inotify/native.rb:1:in `<top (required)>'
        from /home/harsha/gems/gems/rb-inotify-0.10.1/lib/rb-inotify.rb:2:in `require'
        from /home/harsha/gems/gems/rb-inotify-0.10.1/lib/rb-inotify.rb:2:in `<top (required)>'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/adapter/linux.rb:28:in `require'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/adapter/linux.rb:28:in `_configure'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/adapter/base.rb:47:in `block in configure'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/adapter/base.rb:42:in `each'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/adapter/base.rb:42:in `configure'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/adapter/base.rb:66:in `start'
        from /usr/lib/ruby/3.0.0/forwardable.rb:238:in `start'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/listener.rb:71:in `block in <class:Listener>'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/fsm.rb:124:in `instance_eval'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/fsm.rb:124:in `call'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/fsm.rb:105:in `transition_with_callbacks!'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/fsm.rb:72:in `transition'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/listener.rb:92:in `start'
        from /home/harsha/gems/gems/jekyll-watch-2.2.1/lib/jekyll/watcher.rb:26:in `watch'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/build.rb:94:in `call'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/build.rb:94:in `watch'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/build.rb:43:in `process'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/serve.rb:93:in `block in start'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/serve.rb:93:in `each'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/serve.rb:93:in `start'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/serve.rb:75:in `block (2 levels) in init_with_program'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary/command.rb:220:in `block in execute'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary/command.rb:220:in `each'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary/command.rb:220:in `execute'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary/program.rb:42:in `go'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary.rb:19:in `program'
        from /home/harsha/gems/gems/jekyll-3.9.0/exe/jekyll:15:in `<top (required)>'
        from /home/harsha/gems/bin/jekyll:25:in `load'
        from /home/harsha/gems/bin/jekyll:25:in `<top (required)>'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/cli/exec.rb:58:in `load'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/cli/exec.rb:58:in `kernel_load'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/cli/exec.rb:23:in `run'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/cli.rb:451:in `exec'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/vendor/thor/lib/thor/command.rb:28:in `run'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/vendor/thor/lib/thor/invocation.rb:127:in `invoke_command'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/vendor/thor/lib/thor.rb:527:in `dispatch'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/cli.rb:34:in `dispatch'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/vendor/thor/lib/thor/base.rb:584:in `start'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/cli.rb:28:in `start'
        from /home/harsha/gems/gems/bundler-2.5.7/exe/bundle:28:in `block in <top (required)>'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/friendly_errors.rb:117:in `with_friendly_errors'
        from /home/harsha/gems/gems/bundler-2.5.7/exe/bundle:20:in `<top (required)>'
        from /home/harsha/gems/bin/bundle:25:in `load'
        from /home/harsha/gems/bin/bundle:25:in `<main>'
/home/harsha/gems/gems/ffi-1.16.3/lib/ffi.rb:3:in `require': cannot load such file -- 3.0/ffi_c (LoadError)
        from /home/harsha/gems/gems/ffi-1.16.3/lib/ffi.rb:3:in `<top (required)>'
        from /home/harsha/gems/gems/rb-inotify-0.10.1/lib/rb-inotify/native.rb:1:in `require'
        from /home/harsha/gems/gems/rb-inotify-0.10.1/lib/rb-inotify/native.rb:1:in `<top (required)>'
        from /home/harsha/gems/gems/rb-inotify-0.10.1/lib/rb-inotify.rb:2:in `require'
        from /home/harsha/gems/gems/rb-inotify-0.10.1/lib/rb-inotify.rb:2:in `<top (required)>'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/adapter/linux.rb:28:in `require'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/adapter/linux.rb:28:in `_configure'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/adapter/base.rb:47:in `block in configure'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/adapter/base.rb:42:in `each'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/adapter/base.rb:42:in `configure'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/adapter/base.rb:66:in `start'
        from /usr/lib/ruby/3.0.0/forwardable.rb:238:in `start'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/listener.rb:71:in `block in <class:Listener>'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/fsm.rb:124:in `instance_eval'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/fsm.rb:124:in `call'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/fsm.rb:105:in `transition_with_callbacks!'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/fsm.rb:72:in `transition'
        from /home/harsha/gems/gems/listen-3.8.0/lib/listen/listener.rb:92:in `start'
        from /home/harsha/gems/gems/jekyll-watch-2.2.1/lib/jekyll/watcher.rb:26:in `watch'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/build.rb:94:in `call'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/build.rb:94:in `watch'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/build.rb:43:in `process'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/serve.rb:93:in `block in start'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/serve.rb:93:in `each'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/serve.rb:93:in `start'
        from /home/harsha/gems/gems/jekyll-3.9.0/lib/jekyll/commands/serve.rb:75:in `block (2 levels) in init_with_program'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary/command.rb:220:in `block in execute'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary/command.rb:220:in `each'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary/command.rb:220:in `execute'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary/program.rb:42:in `go'
        from /home/harsha/gems/gems/mercenary-0.3.6/lib/mercenary.rb:19:in `program'
        from /home/harsha/gems/gems/jekyll-3.9.0/exe/jekyll:15:in `<top (required)>'
        from /home/harsha/gems/bin/jekyll:25:in `load'
        from /home/harsha/gems/bin/jekyll:25:in `<top (required)>'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/cli/exec.rb:58:in `load'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/cli/exec.rb:58:in `kernel_load'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/cli/exec.rb:23:in `run'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/cli.rb:451:in `exec'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/vendor/thor/lib/thor/command.rb:28:in `run'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/vendor/thor/lib/thor/invocation.rb:127:in `invoke_command'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/vendor/thor/lib/thor.rb:527:in `dispatch'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/cli.rb:34:in `dispatch'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/vendor/thor/lib/thor/base.rb:584:in `start'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/cli.rb:28:in `start'
        from /home/harsha/gems/gems/bundler-2.5.7/exe/bundle:28:in `block in <top (required)>'
        from /home/harsha/gems/gems/bundler-2.5.7/lib/bundler/friendly_errors.rb:117:in `with_friendly_errors'
        from /home/harsha/gems/gems/bundler-2.5.7/exe/bundle:20:in `<top (required)>'
        from /home/harsha/gems/bin/bundle:25:in `load'
        from /home/harsha/gems/bin/bundle:25:in `<main>'
```

I thought of verifying if something is wrong in the `jekyll` itself. So, tried to check the version `jekyll` and it failed with an error

```
  harsha-kadekar.github.io git:(master) ✗ jekyll -v
Ignoring ffi-1.15.5 because its extensions are not built. Try: gem pristine ffi --version 1.15.5
Ignoring ffi-1.15.1 because its extensions are not built. Try: gem pristine ffi --version 1.15.1
Ignoring http_parser.rb-0.6.0 because its extensions are not built. Try: gem pristine http_parser.rb --version 0.6.0
Ignoring commonmarker-0.17.13 because its extensions are not built. Try: gem pristine commonmarker --version 0.17.13
Ignoring ffi-1.15.5 because its extensions are not built. Try: gem pristine ffi --version 1.15.5
Ignoring ffi-1.15.1 because its extensions are not built. Try: gem pristine ffi --version 1.15.1
Ignoring http_parser.rb-0.6.0 because its extensions are not built. Try: gem pristine http_parser.rb --version 0.6.0
Ignoring json-2.5.1 because its extensions are not built. Try: gem pristine json --version 2.5.1
Ignoring racc-1.5.2 because its extensions are not built. Try: gem pristine racc --version 1.5.2
Ignoring unf_ext-0.0.7.7 because its extensions are not built. Try: gem pristine unf_ext --version 0.0.7.7
<internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require': incompatible library version - /home/harsha/gems/gems/ffi-1.16.3/lib/ffi_c.so (LoadError)
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from /home/harsha/gems/gems/ffi-1.16.3/lib/ffi.rb:5:in `rescue in <top (required)>'
        from /home/harsha/gems/gems/ffi-1.16.3/lib/ffi.rb:2:in `<top (required)>'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from /home/harsha/gems/gems/sassc-2.4.0/lib/sassc/native.rb:3:in `<top (required)>'
        from /home/harsha/gems/gems/sassc-2.4.0/lib/sassc.rb:31:in `require_relative'
        from /home/harsha/gems/gems/sassc-2.4.0/lib/sassc.rb:31:in `<top (required)>'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from /home/harsha/gems/gems/jekyll-sass-converter-2.2.0/lib/jekyll/converters/scss.rb:3:in `<top (required)>'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from /home/harsha/gems/gems/jekyll-sass-converter-2.2.0/lib/jekyll-sass-converter.rb:4:in `<top (required)>'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from /home/harsha/gems/gems/jekyll-4.3.3/lib/jekyll.rb:195:in `<top (required)>'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from /home/harsha/gems/gems/jekyll-4.3.3/exe/jekyll:8:in `<top (required)>'
        from /home/harsha/gems/bin/jekyll:25:in `load'
        from /home/harsha/gems/bin/jekyll:25:in `<main>'
<internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require': cannot load such file -- 3.0/ffi_c (LoadError)
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from /home/harsha/gems/gems/ffi-1.16.3/lib/ffi.rb:3:in `<top (required)>'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from /home/harsha/gems/gems/sassc-2.4.0/lib/sassc/native.rb:3:in `<top (required)>'
        from /home/harsha/gems/gems/sassc-2.4.0/lib/sassc.rb:31:in `require_relative'
        from /home/harsha/gems/gems/sassc-2.4.0/lib/sassc.rb:31:in `<top (required)>'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from /home/harsha/gems/gems/jekyll-sass-converter-2.2.0/lib/jekyll/converters/scss.rb:3:in `<top (required)>'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from /home/harsha/gems/gems/jekyll-sass-converter-2.2.0/lib/jekyll-sass-converter.rb:4:in `<top (required)>'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from /home/harsha/gems/gems/jekyll-4.3.3/lib/jekyll.rb:195:in `<top (required)>'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from <internal:/usr/lib/ruby/vendor_ruby/rubygems/core_ext/kernel_require.rb>:85:in `require'
        from /home/harsha/gems/gems/jekyll-4.3.3/exe/jekyll:8:in `<top (required)>'
        from /home/harsha/gems/bin/jekyll:25:in `load'
        from /home/harsha/gems/bin/jekyll:25:in `<main>'
```

As a first step, uninstalled `jekyll` (this was unnecessary )

```
  harsha-kadekar.github.io git:(master) ✗ gem uninstall bundle jekyll
Gem 'bundle' is not installed

Select gem to uninstall:
 1. jekyll-3.9.0
 2. jekyll-4.2.2
 3. jekyll-4.3.3
 4. All versions
> 4
```

Then followed with re-installing `jekyll`

```
  harsha-kadekar.github.io git:(master) ✗ gem install jekyll bundler
Fetching jekyll-4.3.3.gem
Successfully installed jekyll-4.3.3
Parsing documentation for jekyll-4.3.3
Installing ri documentation for jekyll-4.3.3
Done installing documentation for jekyll after 1 seconds
Successfully installed bundler-2.5.7
Parsing documentation for bundler-2.5.7
Done installing documentation for bundler after 0 seconds
2 gems installed
```

```
➜  ~ jekyll -v
Ignoring ffi-1.15.5 because its extensions are not built. Try: gem pristine ffi --version 1.15.5
Ignoring ffi-1.15.1 because its extensions are not built. Try: gem pristine ffi --version 1.15.1
Ignoring http_parser.rb-0.6.0 because its extensions are not built. Try: gem pristine http_parser.rb --version 0.6.0
Ignoring commonmarker-0.17.13 because its extensions are not built. Try: gem pristine commonmarker --version 0.17.13
Ignoring ffi-1.15.5 because its extensions are not built. Try: gem pristine ffi --version 1.15.5
Ignoring ffi-1.15.1 because its extensions are not built. Try: gem pristine ffi --version 1.15.1
Ignoring http_parser.rb-0.6.0 because its extensions are not built. Try: gem pristine http_parser.rb --version 0.6.0
Ignoring json-2.5.1 because its extensions are not built. Try: gem pristine json --version 2.5.1
Ignoring racc-1.5.2 because its extensions are not built. Try: gem pristine racc --version 1.5.2
Ignoring unf_ext-0.0.7.7 because its extensions are not built. Try: gem pristine unf_ext --version 0.0.7.7
jekyll 4.3.3
```

After this, retried running `jekyll` but got a different error.

```
➜  harsha-kadekar.github.io git:(master) ✗ bundle exec jekyll serve --trace
Could not find jekyll-3.9.0 in any of the sources
Run `bundle install` to install missing gems.
```

Followed the recommendation - 

```
➜  harsha-kadekar.github.io git:(master) ✗ bundle install
```

Retried it but got a different error - 

```
  harsha-kadekar.github.io git:(master) ✗ bundle exec jekyll serve --trace
Ignoring commonmarker-0.17.13 because its extensions are not built. Try: gem pristine commonmarker --version 0.17.13
Ignoring ffi-1.15.5 because its extensions are not built. Try: gem pristine ffi --version 1.15.5
Ignoring ffi-1.15.1 because its extensions are not built. Try: gem pristine ffi --version 1.15.1
Ignoring http_parser.rb-0.6.0 because its extensions are not built. Try: gem pristine http_parser.rb --version 0.6.0
Ignoring json-2.5.1 because its extensions are not built. Try: gem pristine json --version 2.5.1
Ignoring racc-1.5.2 because its extensions are not built. Try: gem pristine racc --version 1.5.2
Ignoring unf_ext-0.0.7.7 because its extensions are not built. Try: gem pristine unf_ext --version 0.0.7.7
Could not find compatible versions

Because every version of no-style-please depends on jekyll ~> 3.9.0
  and jekyll ~> 3.9.0 could not be found in locally installed gems,
  no-style-please cannot be used.
So, because Gemfile depends on no-style-please >= 0,
  version solving has failed.
```

Decided to install `3.9` version of `jekyll`

```
  harsha-kadekar.github.io git:(master) gem install jekyll -v 3.9.0
Fetching jekyll-3.9.0.gem
Successfully installed jekyll-3.9.0
Parsing documentation for jekyll-3.9.0
Installing ri documentation for jekyll-3.9.0
Done installing documentation for jekyll after 0 seconds
1 gem installed
```

On retrying, got the same error related to `bundler: failed to load command: jekyll (/home/harsha/gems/bin/jekyll) /home/harsha/gems/gems/ffi-1.16.3/lib/ffi.rb:5:in 'require': incompatible library version - /home/harsha/gems/gems/ffi-1.16.3/lib/ffi_c.so (LoadError)`

On researching, found this reference - 
- [https://stackoverflow.com/questions/29092233/how-to-resolve-loaderror-cannot-load-such-file-ffi-c](https://stackoverflow.com/questions/29092233/how-to-resolve-loaderror-cannot-load-such-file-ffi-c)

Based on that suggestion, re-installed `ffi`

```
  harsha-kadekar.github.io git:(master) ✗ gem install ffi
Building native extensions. This could take a while...
Successfully installed ffi-1.16.3
Parsing documentation for ffi-1.16.3
Installing ri documentation for ffi-1.16.3
Done installing documentation for ffi after 4 seconds
1 gem installed
```

Finally, this worked - 

```
➜  harsha-kadekar.github.io git:(master) ✗ bundle exec jekyll serve --trace
Ignoring commonmarker-0.17.13 because its extensions are not built. Try: gem pristine commonmarker --version 0.17.13
Ignoring ffi-1.15.5 because its extensions are not built. Try: gem pristine ffi --version 1.15.5
Ignoring ffi-1.15.1 because its extensions are not built. Try: gem pristine ffi --version 1.15.1
Ignoring http_parser.rb-0.6.0 because its extensions are not built. Try: gem pristine http_parser.rb --version 0.6.0
Ignoring json-2.5.1 because its extensions are not built. Try: gem pristine json --version 2.5.1
Ignoring racc-1.5.2 because its extensions are not built. Try: gem pristine racc --version 1.5.2
Ignoring unf_ext-0.0.7.7 because its extensions are not built. Try: gem pristine unf_ext --version 0.0.7.7
Configuration file: /home/harsha/workspace/harsha-kadekar.github.io/_config.yml
            Source: /home/harsha/workspace/harsha-kadekar.github.io
       Destination: /home/harsha/workspace/harsha-kadekar.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
       Jekyll Feed: Generating feed for posts
                    done in 0.361 seconds.
 Auto-regeneration: enabled for '/home/harsha/workspace/harsha-kadekar.github.io'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```