<h1 align="center">
  <p><a href="https://github.com/z-shell/zi">
    <img src="https://github.com/z-shell/zi/raw/main/docs/images/logo.svg" alt="Logo" width="60px" height="60px" /></a>
    ❮ ZI ❯ Special Package - Any Gem </p>
</h1>
<h3 align="center">
<table>
    <tr>
        <td><b>Package source:</b></td>
        <td>Source Tarball</td>
        <td>Binary</td>
        <td>Git</td>
        <td>Node</td>
        <td>Gem</td>
    </tr>
    <tr>
        <td><b>Status:</b></td>
        <td>❌</td>
        <td>❌</td>
        <td>❌</td>
        <td>❌</td>
        <td>✔️ (default)</td>
    </tr>
</table></h3><hr />

## The `any-gem` Package

This package is special – it is designed for easy installing of any Ruby Gems locally inside the plugin directory, exposing their binaries via _shims_ (i.e.: forwarder scripts) created automatically by [Bin-Gem-Node](https://github.com/z-shell/z-a-bin-gem-node) annex.

The Ruby Gem(s) to install are specified by the `param'GEM → {gem1}; GEM2 → {gem2}; …'` ice. The name of the plugin will be `{gem1}`, unless `id-as''` ice will be provided, or the `IDAS` param will be set (i.e.: `param'IDAS → my-plugin; GEM → …'`).

A few example invocations:

```shell
# Install `chef` Gem and call the plugin with the same name
zi pack param='GEM → chef' for any-gem
```

```shell
# Install `rails' Gem and call the plugin: ruby-on-rails
zi id-as=ruby-on-rails pack param='GEM → rails' for any-gem
```

```shell
# Install `jekyll` Gem and call the plugin: jkl
zi pack param='IDAS → jkl; GEM → jekyll' for any-gem
```

## Default Profile

The only profile that does all the magic. It relies on the `%PARAM%` keywords, which are substituted with the `value` from the ice `param'PARAM → value; …'`.

The ZI command executed will be equivalent to:

```shell
zi lucid id-as="${${:-%IDAS%}:-%GEM%}" as=null \
  gem="%GEM%;%GEM2%;%GEM3%;%GEM4%;%GEM5%;%GEM6%;%GEM7%;%OTHER%" \
  sbin="n:bin/*" for \
    z-shell/null
```

---

> This repository compatible with [ZI](https://github.com/z-shell/zi)

The [ZI](https://github.com/z-shell/zi) package that can use the [zsh-string-lib](https://github.com/z-shell/zsh-string-lib) to automatically:

- get the plugin's Git repository OR release-package URL,
- get the list of the recommended ices for the plugin,
  - there can be multiple lists of ices,
  - the ice lists are stored in _profiles_; there's at least one profile, _default_,
  - the ices can be selectively overridden.
