---
title: "Deploying a website built with Hugo to GitHub Pages"
description: "My workflow to deploy a gohugo static website using TravisCI and GitHub Pages hosting."
date: 2018-07-13T16:00:00+02:00
draft: false
---

I've been building some static websites using GitHub pages. The flow is
_roughly_ always the same: code is pushed to the `master` branch, continuous
integration tool kicks in, and result is published to the `gh-pages` branch.

That sounds quite simple, but there are a few dozens of ways to do it, and I
feel like I've managed over the last few years to build my (probably shared with
thousands of developers) own decent way of doing it using
[TravisCI](https://travis-ci.com/). However, I always forget something in the
process, which is pretty much frustrating.

This is the good time for a change and write down all the steps for myself.

## A bit of configuration

To push the production build to the `gh-pages` branch, TravisCI needs a GitHub
[access token](https://github.com/settings/tokens). Once generated, this token
has to be added to the TravisCI configuration.

Using TravisCI dashboard to achieve this is fine and requires no local
installation. But if you don't mind installing some stuff, this can be done
using the command line. The
[`travis` gem](https://github.com/travis-ci/travis.rb) perfectly serves that
purpose (among a million of other things), and it can both encrypt the token and
append it to the `travis.yml` configuration file. Encrypting the access token is
obvious for security reasons, nobody wants it to be stored in clear text.

```sh
gem install travis
travis encrypt -r github_username/repository_name GITHUB_TOKEN=the_github_token --add
```

Note that if this command is ran in a directory under git control and the `-r`
is omitted, `travis` will ask to tie the encrypted string with the current
repository.

## Setting up continuous integration

Continuous integration is split in 2 parts: build and deploy.

The build part mostly depends on the publishing tool, but
[the build lifecycle](https://docs.travis-ci.com/user/customizing-the-build/#The-Build-Lifecycle)
remains the same. For Hugo, I find that installing via the Debian package is the
most straightforward way to do it, and it requires no additional software.

About the deploy part, if one simply needs to push to the GitHub `gh-pages`
branch, I recommend using the
[_pages_ provider](https://docs.travis-ci.com/user/deployment/pages/). It's dead
simple to configure and requires no scripting at all. If more tuning before
pushing is required (one may way to push to a different branch or remote for
instance) is needed, using the `script` provider is fine.

### TravisCI configuration with _pages_ provider

Travis configuration may vary, but the one I use is fairly simple for a Hugo
website:

```yaml
# sudo is required to install hugo deb package
sudo: true
env:
  global:
  - GITHUB_REPO: github_username/repository_name
  - secure: encrypted_token

# fetch archive and install
install:
- wget https://github.com/gohugoio/hugo/releases/download/v0.25.1/hugo_0.25.1_Linux-64bit.deb
- sudo dpkg -i hugo_0.25.1_Linux-64bit.deb

# show current hugo version and build website
script:
- hugo version
- hugo

deploy:
  # don't remove build directory so it can be pushed later
  skip_cleanup: true
  # this provider makes all the work for us
  provider: pages
  local_dir: public
  repo: $GITHUB_REPO
  github_token: $GITHUB_TOKEN
  # using fqdn will add the CNAME file
  fqdn: www.domain.com
  # only deploy if commits are pushed to master
  on:
    branch: master
```

For a Jekyll website, I use about the same file with very minor changes:

```yaml
sudo: false
language: ruby
rvm:
- 2.2.4
env:
  global:
  - GITHUB_REPO: github_username/repository_name
  - secure: encrypted_token
script: bundle exec jekyll build && bundle exec rake test
deploy:
  skip_cleanup: true
  provider: pages
  local_dir: _site
  repo: $GITHUB_REPO
  github_token: $GITHUB_TOKEN
  fqdn: www.domain.com
  on:
    branch: master
```

### Legacy deploy script example

I used to deploy using the `script` provider to achieve a less good result. Code
was indeed pushed to `gh-pages` branch with a commit message, but the `pages`
provider does some extra stuff I don't want to code: add the CNAME file, create
a file with build date... Anyway, I archived that script for the record.

```bash
#!/bin/bash

set -e

# remove version control
rm -rf .git
cd public

# initialize a repository in the build directory
git init

# set a few variables to let GitHub know who is pushing commits
git config --global user.email $GIT_EMAIL
git config --global user.name $GIT_NAME

# configure the remote repository
git remote add origin https://$GITHUB_TOKEN@github.com/$GITHUB_REPO.git
git add .

# commit and push to remote gh-pages branch
git commit -m "Deploy to GitHub Pages (travis build #$TRAVIS_BUILD_NUMBER)"
git push --force --quiet origin HEAD:gh-pages
```

---
