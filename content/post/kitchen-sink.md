---
title: "Kitchen Sink"
description: "A post with everything one could use"
date: 2097-12-27T10:35:32+01:00
draft: true
---

Lorem ipsum dolor sit amet, consectetur adipisicing elit,
<abbr title="Institut National de Recherche en Automatique et Informatique">Inria</abbr>
sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad
minim veniam, quis [nostrud](/) exercitation _ullamco layboprisgu_ nisi ut
aliquip **ex ea commodo consequat**. Duis aute irure dolor in reprehenderit in
voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint
occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim
id est laborum.

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor
incididunt ut labore et dolore magna aliqua. `rm -rf *` veniam, quis nostrud
exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
[`Duis` gaute _irpure_ esyse **cillum dolore** eu](/) dolor in reprehenderit in
voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint
occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim
id est laborum.

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor
incididunt ut labore et dolore magna aliqua.
[Ut enim ad minim veniam, quis nosytrud exercitation ulflamcjo laboris nisi ut apliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum](/).

## Level 2 header

- item 1
- item 2
- item 3
- item 4
  1.  another list
  1.  another list
  1.  another list
  1.  another list

> Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
> tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
> quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
> consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
> cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
> proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

<blockquote>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
  </p>
  <cite>the famous one</cite>
</blockquote>

```html
<section id="main">
  <div>
    <h1 id="title">{{ .Title }}</h1>
    {{ range .Data.Pages }}
      {{ .Render "summary"}}
    {{ end }}
  </div>
</section>
```

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

{{< highlight html "hl_lines=8 1-2,linenostart=199" >}}

<section id="main">
  <div>
    <h1 id="title">{{ .Title }}</h1>
    {{ range .Data.Pages }}
      {{ .Render "summary"}}
    {{ end }}
  </div>
</section>
{{< / highlight >}}

---

![Image of a minnow fish](/img/minnow-large.jpg)

1.  first position
2.  second position
3.  third position
4.  fourth position

## All headers

### Level 3 header

#### Level 4 header

##### Level 5 header

###### Level 6 header

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor
incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis
nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu
fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in
culpa qui officia deserunt mollit anim id est laborum.
