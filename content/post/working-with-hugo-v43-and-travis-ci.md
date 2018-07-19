---
title: "Working with Hugo v43 and TravisCI"
description: "Hugo v43 has a new assets pipeline that requires some updates to the travis configuration. I'll walk through the steps to make it work properly."
date: 2018-07-19T12:00:00+02:00
draft: true
---

Since Hugo v43, you can use a brand new assets pipeline called
[Hugo Pipes](http://gohugo.io/news/0.43-relnotes/) that allows using SASS/SCSS
files without relying on another build tool such as [Gulp](https://gulpjs.com/)
or [Grunt](https://gruntjs.com/).

However, updating Hugo and your code to use Pipes will not work out of the box.

This post is a follow up of my ["Publishing a website built with Hugo to GitHub
Pages"]({{< relref "post/publishing-a-static-website.md" >}}) post.

## Pipes require the extended version of Hugo

> Hugo is now released with two binary version: One with and one without
> SCSS/SASS support. At the time of writing, this is only available in the
> binaries on the GitHub release page. Brew, Snap builds etc. will come. But
> note that you only need the extended version if you want to edit SCSS. For
> your CI server, or if you don’t use SCSS, you will most likely want the
> non-extended version.

This means this change also need to be applied to the `.travis.yml`
configuration file.

If you use a Mac, Homebrew will install the extended version of Hugo.

## Pipes expect node and some npm libraries to be installed

Some of the assets pipeline logic relies on a couple of node packages, and even
if you don't use them, Hugo won't build unless they are installed.

First I initialized the `package.json` file with `npm init`.

Them, as I tend to never install an npm package globally, I just installed the
dependencies locally for this project running `npm i postcss-cli autoprefixer`.

This step generates a couple of files, don't forget to add them to the
`.gitignore`.

## Processing steps require a bit of configuration

To use [PostCSS](https://postcss.org/) and
[autoprefixer](https://github.com/postcss/autoprefixer), some configuration
files must be created. The ones at the root of this project have the bare
minimum configuration and should be enough for most of my needs later.

## Caveats

### Files location

I used to have my css file in the `static` directory of my theme, but to be used
as a resource, the file has to be in the assets folder of the theme.

### Missing libraries

While everything worked perfectly fine locally, I had trouble running the
extended version of Hugo on Travis environment. The script step shown
`GLIBCXX_3.4.20' not found` errors, and checking what GLIBCXX were in the shared
objects, I got the following:

```sh
$ strings /usr/lib/x86_64-linux-gnu/libstdc++.so.6 | grep GLIBCXX
GLIBCXX_3.4
GLIBCXX_3.4.1
GLIBCXX_3.4.2
GLIBCXX_3.4.3
GLIBCXX_3.4.4
GLIBCXX_3.4.5
GLIBCXX_3.4.6
GLIBCXX_3.4.7
GLIBCXX_3.4.8
GLIBCXX_3.4.9
GLIBCXX_3.4.10
GLIBCXX_3.4.11
GLIBCXX_3.4.12
GLIBCXX_3.4.13
GLIBCXX_3.4.14
GLIBCXX_3.4.15
GLIBCXX_3.4.16
GLIBCXX_3.4.17
GLIBCXX_3.4.18
GLIBCXX_3.4.19
GLIBCXX_DEBUG_MESSAGE_LENGTH
```

Installing `libstdc++-4.9-dev` did better:

```sh
$ strings /usr/lib/x86_64-linux-gnu/libstdc++.so.6 | grep GLIBCXX
GLIBCXX_3.4
GLIBCXX_3.4.1
GLIBCXX_3.4.2
GLIBCXX_3.4.3
GLIBCXX_3.4.4
GLIBCXX_3.4.5
GLIBCXX_3.4.6
GLIBCXX_3.4.7
GLIBCXX_3.4.8
GLIBCXX_3.4.9
GLIBCXX_3.4.10
GLIBCXX_3.4.11
GLIBCXX_3.4.12
GLIBCXX_3.4.13
GLIBCXX_3.4.14
GLIBCXX_3.4.15
GLIBCXX_3.4.16
GLIBCXX_3.4.17
GLIBCXX_3.4.18
GLIBCXX_3.4.19
GLIBCXX_3.4.20
GLIBCXX_3.4.21
GLIBCXX_3.4.22
GLIBCXX_3.4.23
GLIBCXX_3.4.24
GLIBCXX_3.4.25
GLIBCXX_DEBUG_MESSAGE_LENGTH
```

But I was not quite done yet, and the build returned a
`relocation error: hugo: symbol _ZTVNSt7__cxx1119basic_istringstreamIcSt11char_traitsIcESaIcEEE, version GLIBCXX_3.4.21 not defined in file libstdc++.so.6 with link time reference`
error.

At this point I was kind of lost and went to seek support on the Hugo discussion
forum
([see the thread](https://discourse.gohugo.io/t/hugo-v44-extended-and-relocation-errors/13029)).
