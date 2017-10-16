---
layout: post
title: Hello World - Vno
date: 2016-02-16 15:32:24.000000000 +09:00
---

#### What's this

[Vno Jekyll](https://github.com/onevcat/vno-jekyll) is a theme for [Jekyll](http://jekyllrb.com). It is a port of my Ghost theme [vno](https://github.com/onevcat/vno), which is originally developed from [Dale Anthony's Uno](https://github.com/daleanthony/uno).

#### Usage

```bash
$ git clone https://github.com/onevcat/vno-jekyll.git your_site
$ cd your_site
$ bundler install
$ bundler exec jekyll serve
```

Your site with `Vno Jekyll` enabled should be accessible in http://127.0.0.1:4000.

For more information about Jekyll, please visit [Jekyll's site](http://jekyllrb.com).

`sudo apt install ruby-bundler`
`sudo apt install jekyll`
`sudo apt install ruby-dev`
`gem install public_suffix`



### Problem

版本兼容性问题：

1.  listen 版本3.1.5, 太新了，不是发布版本。

   /var/lib/gems/2.3.0/gems/listen-3.1.5/lib/listen.rb

     *`Dependency Error: Yikes! It looks like you don't have jekyll-watch or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- ruby_dep/warning' If you run into trouble, you can find helpful resources at https://jekyllrb.com/help/!`* 

   说是jekyll-watch未安装，其实是listen.rb 3.1.5报异常，日志的调用信息不准确。

   0.8版本ok。

2. rouge版本太旧， 1.0.0 ， 导致页面跳转异常。  3.0.0 版本ok。



用 bundler install 安装依赖比较好。gem安装包的特定版本，可以执行如下命令：

`sudo gem uninstall listen:3.1.5`



#### Configuration

All configuration could be done in `_config.yml`. Remember you need to restart to serve the page when after changing the config file. Everything in the config file should be self-explanatory.

#### Background image and avatar

You could replace the background and avatar image in `assets/images` folder to change them.

#### Sites using Vno

[My blog](http://onevcat.com) is using `Vno Jekyll` as well, you could see how it works in real. There are some other sites using the same theme. You can find them below:

| Site Name  | URL                                      |
| ---------- | ---------------------------------------- |
| OneV's Den | [http://onevcat.com](http://onevcat.com) |
| July Tang  | [http://blog.julytang.xyz](http://onevcat.com) |
| Harry Lee  | [http://qiuqi.li](http://qiuqi.li)       |

> If you happen to be using this theme, welcome to [send me a pull request](https://github.com/onevcat/vno-jekyll/pulls) to add your site link here. :)

#### License

Great thanks to [Dale Anthony](https://github.com/daleanthony) and his [Uno](https://github.com/daleanthony/uno). Vno Jekyll is based on Uno, and contains a lot of modification on page layout, animation, font and some more things I can not remember. Vno Jekyll is followed with Uno and be licensed as [Creative Commons Attribution 4.0 International](http://creativecommons.org/licenses/by/4.0/). See the link for more information.
