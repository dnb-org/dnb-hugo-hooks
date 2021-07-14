[![GitHub issues](https://img.shields.io/github/issues-raw/dnb-org/hooks?logo=github&style=for-the-badge)](https://github.com/dnb-org/hooks/issues) ![LasCHanges](https://img.shields.io/github/last-commit/dnb-org/hooks?color=%23ff7700&logo=github&style=for-the-badge) [![Codacy Badge](https://img.shields.io/codacy/grade/1aa52a19ae5b42efa80f04157a29ae8d?logo=codacy&style=for-the-badge)](https://www.codacy.com/gh/dnb-org/hooks/dashboard) ![License](https://img.shields.io/github/license/dnb-org/hooks?logo=github&style=for-the-badge) ![Follow us on Twitter](https://img.shields.io/twitter/follow/hugonewsletter?color=%231DA1F2&logo=twitter&style=for-the-badge) [![Gitter Chatroom](https://img.shields.io/gitter/room/dnb-org/community?color=%23ed1965&logo=gitter&style=for-the-badge)](https://gitter.im/dnb-org/community) ![Latest Version](https://img.shields.io/github/v/tag/dnb-org/hooks?color=%23ed1965&label=Release&logo=hugo&logoColor=%23ffffff&sort=semver&style=for-the-badge) [![Hugo Version](https://img.shields.io/badge/Hugo-0.84.0-%23ed1965&?style=for-the-badge&logo=hugo&color=ed1965&?cacheSeconds=maxAge)](https://gohugo.io/)

## dnb-org Hooks

This is a template hooks system for Hugo.

We often want to add places in our templates that users can add something on
their own. Be it some code for an analytics program or additional footer
sections, a banner at the top of the page or some arbitrary Javascript code.

This layout introduces hooks. A simple way a theme developer can add these
"layout locations" to hook additional features in.

### Hook use

Hooks are saved to the `layouts/partials/hooks` directory. There are no errors 
if a hook is not found. If a hook has an added `-cached` to it's name then it will
be cached and on multiple calls re-used. 

For example:

```gotemplate
{{ partial "func/hook" "head-start" }}
```

will load `layouts/partials/hooks/head-start.html` and `layouts/partials/hooks/head-start-cached.html`.

You can force caching by loading the hook via `partialCached` instead.

Hooks do not return any values, they execute layouts. 

### Simple Use

Add the hook name as parameter to simple calls. The context inside of the hook
layout will have a hook parameter with that name.

```gotemplate
{{- partial "func/hook" "hookname" -}}
{{- partialCached "func/hook" "hookname" -}}
```

### Extended Use

If you want to submit more information than just the hookname (like the context)
then add a `dict` as parameter. The `hook` item is required, everything else
will be passed through to the hook layout.

```gotemplate
{{- partial "func/hook" ( dict "hook" "hookname" "context" . ) -}}
{{- partialCached "func/hook" ( dict "hook" "hookname" "context" . ) -}}
```

### Some more configuration

The hook will add a warning (more like a notification, but Hugo does not have
anything like that yet) if a hook exists that is not used. You can disable this
by setting `Params.dnb.hooks.debug` to any value lower than 4.

### Installation

Enable modules in your own repository and add this module to your required modules in config.toml:

```shell script
hugo mod init github.com/username/reponame
```

Then add the module to your configuration:

```toml
[module]
[[module.imports]]
path = "github.com/dnb-org/hooks"
```

The next time you run hugo it will download the latest version of the module.

### Update

```shell script
# to update this module:
hugo mod get -u github.com/dnb-org/hooks

# to update all modules:
hugo mod get -u

# to update all modules recursively:
hugo mod get -u ./...
```
