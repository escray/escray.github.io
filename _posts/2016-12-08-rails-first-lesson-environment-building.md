---

layout: post
title: Rails 第一课：环境建置
date: 2016-12-08

---

本来是打算写一篇报错记录的，不过后来发现这个内容可能更适合写一篇学习记录。

## Objective

关于 Rails 第一课，环境建置，现在能够回想起来的就是在安装 Rails 5.0 的时候遇到了一点麻烦，并解决掉了。

因为之前也看过一些 Rails 的教程，搭建过开发环境，所以再次进行配置的时候遇到“Ignoring nokogiri-1.6.8.1 because its extensions are not built.”报错信息，后来在 Google 和 StackOverflow 的帮助下，解决了问题。

另外就是比较偶尔的遇到了 heroku.com 的维护，大概是在 12月7日 的早上，不过对我并没有什么太大的影响，稍等了一会儿就好。

## Reflective

完成第一课之后，感觉很不错，算是全栈营的一小步，个人成长一大步吧。

高峰在于最终解决了所有遇到的问题，完成了第一课的内容。

低点在于遇到不好环境配置的问题，以至于有点怀疑自己。

## Interpretive

学到的是如何搭建 rails 开发环境，并且配合 heroku 进行发布。

今天的重要领悟应该是关于 XDite 老师推荐的两篇文章。之前自己在学习编程的过程中，也有过“从入门到放弃”，进而有点绝望的感觉。这次打算放弃“傲慢”，听从老师指示，按要求完成作业，重复练习，争取在完成在线课程之后，进入线下课程学习。

大钱已经付了，我相信 XDite 是足够好的老师，并且我愿意认真对待这门课程，接下来就是模仿和重复练习了。

## Decisional

用一句话来形容的话，应该是“前路漫漫，上下求索，乐在其中”。

之后需要努力的是在 1月3日 之前，每天保证大约 1-2 个小时的时间用于全栈营的课程，完成前三课的内容。

## 学习记录

安装 xcode 的时候发现需要下载大概 4.47 GB 的安装包，心中一惊，不过好在网速还不错。

因为之前配置过 xcode 的 Command Line Tools，在安装 xcode 之前，执行

```
$ xcode-select -p
```

得到路径是： /Applications/Xcode.app/Contents/Developer

而不是： /Library/Developer/CommandLineTools

安装之后，得到：/Applications/Xcode.app/Contents/Developer

之前安装过 Homebrew，不过在更新 Homebrew 的时候遇到权限不足的报错信息，解决过程如下：

```
$ brew update
Error: /usr/local is not writable. You should change the ownership
and permissions of /usr/local back to your user account:
  sudo chown -R $(whoami) /usr/local

$ sudo brew update
Password:
Error: Cowardly refusing to 'sudo brew update'
You can use brew with sudo, but only if the brew executable is owned by root.
However, this is both not recommended and completely unsupported so do so at
your own risk.

$ sudo chown -R $(whoami) /usr/local

$ brew update
```

可能是因为当时正在下载 xcode，所以等了很久都没有提示信息，第二天早上看到了如下提示：

```
Error: You have not agreed to the Xcode license. Please resolve this by running:
  sudo xcodebuild -license accept
```

接下来，继续更新 Homebrew

```
$ sudo xcodebuild -license accept
Password:

$ xcode-select -p
/Applications/Xcode.app/Contents/Developer

$ brew update
Updated 1 tap (caskroom/cask).
No changes to formulae.
==> Migrating HOMEBREW_REPOSITORY (please wait)...
==> Migrated HOMEBREW_REPOSITORY to /usr/local/Homebrew!
Homebrew no longer needs to have ownership of /usr/local. If you wish you can
return /usr/local to its default ownership with:
  sudo chown root:wheel /usr/local

$ brew update
Already up-to-date.

$ sudo chown root:wheel /usr/local
```

然后就是高潮时段，安装 rails 5.0 的曲折经历。

```
$ gem install rails -v 5.0.0
/Users/escray/.rvm/rubies/ruby-2.3.1/lib/ruby/2.3.0/rubygems/core_ext/kernel_require.rb:55:in `require': incompatible library version - /Users/escray/.rvm/gems/ruby-2.3.1/gems/io-console-0.4.6/lib/io/console.bundle (fatal)
     from /Users/escray/.rvm/rubies/ruby-2.3.1/lib/ruby/2.3.0/rubygems/core_ext/kernel_require.rb:55:in `require'
     from /Users/escray/.rvm/rubies/ruby-2.3.1/lib/ruby/2.3.0/rubygems/user_interaction.rb:9:in `<top (required)>'
```

第一次遇到报错信息，没有关系，用管理员权限再次安装。

```
$ sudo gem install rails -v 5.0.0
Password:
Fetching: i18n-0.7.0.gem (100%)
Successfully installed i18n-0.7.0
……
Parsing documentation for sprockets-rails-3.2.0
Installing ri documentation for sprockets-rails-3.2.0
Parsing documentation for rails-5.0.0
Installing ri documentation for rails-5.0.0
Done installing documentation for i18n, thread_safe, tzinfo, concurrent-ruby, activesupport, rack, rack-test, mini_portile2, nokogiri, loofah, rails-html-sanitizer, rails-dom-testing, builder, erubis, actionview, actionpack, activemodel, arel, activerecord, globalid, activejob, mime-types-data, mime-types, mail, actionmailer, nio4r, websocket-extensions, websocket-driver, actioncable, thor, method_source, railties, bundler, sprockets, sprockets-rails, rails after 54 seconds
36 gems installed
```

安装过程很顺利，不过终于遇到了本课的“大Boss”，nokogiri 错误

```
⇒  rails -v
Ignoring nokogiri-1.6.8.1 because its extensions are not built.  Try: gem pristine nokogiri --version 1.6.8.1

    Rails 5 requires Ruby 2.2.2 or newer.

    You're running
      ruby 2.0.0p648 (2015-12-16 revision 53162) [universal.x86_64-darwin16]

    Please upgrade to Ruby 2.2.2 or newer to continue.
```

放狗，发现有不少人遇到类似的情况，一下是我的解决过程

```
⇒  gem pristine nokogiri --version 1.6.8.1
Restoring gems to pristine condition...
ERROR:  While executing gem ... (Errno::EACCES)
    Permission denied @ rb_sysopen - /Users/escray/.rvm/rubies/ruby-2.3.1/lib/ruby/gems/2.3.0/gems/nokogiri-1.6.8.1/.autotest

⇒  sudo gem pristine nokogiri --version 1.6.8.1
Password:
ERROR:  While executing gem ... (Gem::Exception)
    Failed to find gems ["nokogiri"] = 1.6.8.1

⇒  rvm list

rvm rubies

=* ruby-2.3.1 [ x86_64 ]

# => - current
# =* - current && default
#  * - default

/Users/escray/.rvm/bin/rvm: line 66: shell_session_update: command not found

$ sudo rails -v
Password:
Rails 5.0.0
```

看上去在管理员账户下，rails 5.0 是可以用的，而在一般权限下有问题。那么按照网上的提示首先更新 gem 和 xcode

```
⇒  gem update --system
Updating rubygems-update
Fetching: rubygems-update-2.6.8.gem (100%)
Successfully installed rubygems-update-2.6.8
……

escray@escrays-MacBook-Pro:~|⇒  xcode-select --install
xcode-select: error: command line tools are already installed, use "Software Update" to install updates

escray@escrays-MacBook-Pro:~|⇒  xcode-select --update
xcode-select: error: invalid argument '--update'
Usage: xcode-select [options]

http://www.nokogiri.org/tutorials/installing_nokogiri.html#mac_os_x
```

尝试按照指定目录安装 nokogiri，结果还是没有成功。

```
⇒  gem install nokogiri -- --use-system-libraries --with-xml2-config=/usr/local/opt/libxml2/include/libxml2 
    --with-xslt-config=/path/to/xslt-config

⇒  gem install nokogiri -- --use-system-libraries  --with-xml2-include=$(brew --prefix libxml2)/include/libxml2

⇒  rails -v
Ignoring nokogiri-1.6.8.1 because its extensions are not built.  Try: gem pristine nokogiri --version 1.6.8.1

    Rails 5 requires Ruby 2.2.2 or newer.

    You're running
      ruby 2.0.0p648 (2015-12-16 revision 53162) [universal.x86_64-darwin16]

    Please upgrade to Ruby 2.2.2 or newer to continue.
```

因为发现总是提示 Ruby 版本的问题，所以尝试重新安装 Ruby 2.3.1

```
⇒  rvm reinstall 2.3.1

/Users/escray/.rvm/bin/rvm: line 66: shell_session_update: command not found
```

为了解决上面一行的报错信息，执行如下命令：

```
⇒ source ~/.rvm/scripts/rvm

⇒  gem install rails -v 5.0.0
Ignoring executable-hooks-1.3.2 because its extensions are not built.  Try: gem pristine executable-hooks --version 1.3.2
Ignoring gem-wrappers-1.2.7 because its extensions are not built.  Try: gem pristine gem-wrappers --version 1.2.7
Error loading RubyGems plugin "/Users/escray/.rvm/gems/ruby-2.3.1@global/gems/executable-hooks-1.3.2/lib/rubygems_plugin.rb": cannot load such file -- executable-hooks/wrapper (LoadError)
Error loading RubyGems plugin "/Users/escray/.rvm/gems/ruby-2.3.1@global/gems/gem-wrappers-1.2.7/lib/rubygems_plugin.rb": cannot load such file -- gem-wrappers (LoadError)
Fetching: thread_safe-0.3.5.gem (100%)
Successfully installed thread_safe-0.3.5
```

最终解决问题的，其实是使用了如下命令：

```
⇒  rvm use ruby-2.3.1@rails5.0 --create 
```

我的理解是又创建了一个 使用 ruby 2.3.1 的 shell 环境。然后在这个环境下，再次安装 rails 5.0

```
⇒  gem update --system
⇒  gem install rails -v 5.0.0
```

至此，基本解决了我所遇到这个问题。