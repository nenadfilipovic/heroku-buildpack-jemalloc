# Heroku Buildpack: Jemmaloc

[Jemalloc](http://jemalloc.net/) is a general purpose malloc implementation
that works to avoid memory fragmentation in multithreaded applications. This
buildpack makes it easy to install and use jemalloc on Heroku and compatible
platforms.

## Install

    # Add buildpack to your instance.
    - Via website: nenadfilipovic/heroku-buildpack-jemalloc
    - Via cli: heroku buildpacks:add nenadfilipovic/heroku-buildpack-jemalloc

    # Push changes to deploy.
    $ git push

## Usage

### Recommended

Set the JEMALLOC_ENABLED config option to true and jemalloc will be used for
all commands run inside of your dynos.

```console
heroku config:set JEMALLOC_ENABLED=true
```

### Per dyno

To control when jemalloc is configured on a per dyno basis use
`jemalloc.sh <cmd>` and ensure that JEMALLOC_ENABLED is unset.

Example Procfile:

```yaml
web: jemalloc.sh bundle exec puma -C config/puma.rb
```

## Configuration

### JEMALLOC_ENABLED

Set this to true to automatically enable jemalloc.

```console
heroku config:set JEMALLOC_ENABLED=true
```

To disable jemalloc set the option to false. This will cause the application to
restart disabling jemalloc.

```console
heroku config:set JEMALLOC_ENABLED=false
```

### JEMALLOC_VERSION

Set this to select or pin to a specific version of jemalloc. The default is to
use the latest stable version if this is not set. You will receive an error
mentioning tar if the version does not exist.

#### Available Versions

| Version                                                          | Released   |
| ---------------------------------------------------------------- | ---------- |
| [3.6.0](https://github.com/jemalloc/jemalloc/releases/tag/3.6.0) | 2015-04-15 |
| [4.0.4](https://github.com/jemalloc/jemalloc/releases/tag/4.0.4) | 2015-10-24 |
| [4.1.1](https://github.com/jemalloc/jemalloc/releases/tag/4.1.1) | 2016-05-03 |
| [4.2.1](https://github.com/jemalloc/jemalloc/releases/tag/4.2.1) | 2016-06-08 |
| [4.3.1](https://github.com/jemalloc/jemalloc/releases/tag/4.3.1) | 2016-11-07 |
| [4.4.0](https://github.com/jemalloc/jemalloc/releases/tag/4.4.0) | 2016-12-04 |
| [4.5.0](https://github.com/jemalloc/jemalloc/releases/tag/4.5.0) | 2017-02-28 |
| [5.0.1](https://github.com/jemalloc/jemalloc/releases/tag/5.0.1) | 2017-07-01 |
| [5.1.0](https://github.com/jemalloc/jemalloc/releases/tag/5.1.0) | 2018-05-08 |
| [5.2.0](https://github.com/jemalloc/jemalloc/releases/tag/5.2.0) | 2019-04-02 |
| [5.2.1](https://github.com/jemalloc/jemalloc/releases/tag/5.2.1) | 2019-08-05 |
| [5.3.0](https://github.com/jemalloc/jemalloc/releases/tag/5.3.0) | 2022-05-06 |

**Default**: `5.3.0`

**note:** This setting is only used during slug compilation. Changing it will
require a code change to be deployed in order to take affect.

```console
heroku config:set JEMALLOC_VERSION=3.6.0
```
