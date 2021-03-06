---
title: Using ASDF-vm
subtitle: Solve All of Your Version Problems
date: 2017-05-23
author: Connor Rigby
draft: false
tags: ["nerves"]
---

Nerves usually pushes the bleeding edge of Elixir, which means we sometimes
sometimes hear about problems in our Nerves Slack channel that can be solved by
updating to the latest version of Elixir and OTP. Now, there are built-in options in most operating systems to do this, such as
`brew`, `apt-get`, `pacman` etc, and they all work with varying levels of success. ASDF-vm is an alternate version manager that allows easy installation and switching between different versions of various packages.

<!--more-->

# Managing Elixir and Erlang with ASDF-vm
Let's go through how easy it is to set up Elixir and Erlang with ASDF.

## Instalation
You pretty much will just need `git` for installation.
``` bash
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.3.0
source ~/.asdf/asdf.sh
```

Then you will want to install the `plugin`s for both Erlang and Elixir

## Install Plugins
``` bash
asdf plugin-add erlang https://github.com/asdf-vm/asdf-erlang.git
asdf plugin-add elixir https://github.com/asdf-vm/asdf-elixir.git
```

## Choose Versions
``` bash
asdf install erlang 19.2 # This one can take a while, depending on your machine
asdf install elixir 1.4.2
```

## Setup
``` bash
asdf global erlang 19.2
asdf global elixir 1.4.2
```

## Updating
When a new stable release comes out, you can do similar commands. Heres the OTP 20/ Elixir 1.4.4 example:
``` bash
asdf install erlang 20
asdf install elixir 1.4.4

asdf global erlang 20
asdf global elixir 1.4.4
```

Then, when that inevitably breaks, you can simply change back:
``` bash
asdf global erlang 19.3
asdf global elixir 1.4.2
```

## Nerves
The Nerves Project currently builds ERTS (Erlang Run Time System) into the officially-supported systems. The build tools will throw an error if the host machine's OTP vesion doesn't match the version built into the system for your target.
This is done to ensure you can develop your application on your host machine, then push to your embedded device and everything will work as expected. This is where a version manager really comes in handy. Instead of sifting thru `.deb` files, or trying to install a newer or older version of OTP using your operating system's package manager, you can run two commands that explicitly explain the version of a package you want.
