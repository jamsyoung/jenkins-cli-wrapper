# Jenkins CLI Wrapper

Jenkins has a CLI. You can download it from your Jenkins instance.

> Jenkins > Manage > Jenkins CLI

It does many things. One is very useful for tailing a build log from the console.
It's syntax is hard on the fingers though. It goes like this:

```shell
$ java -jar [path/to/downloaded/jenkins-cli.jar] \
    -s [https://url-to-jenkins-server/] \
    -auth [your-jenkins-username]:[your-very-long-jekins-api-token]
    console [jenkins-build-plan]/[source-branch] \
    [build-number] \
    -f
```

WoW! right?!?

This _Jenkins CLI Wrapper_ is currently only a wrapper for the single `console` command.

```shell
$ ./jenkins --job [jenkins-build-plan]/[source-branch] -f
```

So much easier!

When run for the first time, some questions will be asked with the answers stored in `~/.jenkinsrc`.
This file holds the following settings:

- `jenkins_api_token`
- `jenkins_cli_jar_path`
- `jenkins_url`
- `jenkins_user`

> ☝️ Your Jenkins API Token can be created in your Jenkins instance at:  
> Jenkins > Your Account > Configure > API Token > Add new token

## Usage

```shell
jenkins --job jenkins-job/source-branch [--build N] [--follow | --display-last n]
```

```shell
$ ./jenkins --help

Usage:
  jenkins --job jenkins-job/source-branch [--build N] [--follow | --display-last N]

Required Options:
    -j | --job            Job format is buildplan/branch

Misc Options:
    -b | --build          Jenkins build number; defaults to lastBuild
    -f | --follow         If the build is in progress, append console output as it comes
    -n | --display-last   Display the last N lines

    -h | --help           Show help and version information
    -v | --version        Show help and version information

Examples viewing the results of build plan `autopwn` on branch `master`:
  jenkins --job autopwn/master
  jenkins --job autopwn/master --follow
  jenkins --job autopwn/master --display-last 10
  jenkins --job autopwn/master --build 3 --follow
  jenkins --job autopwn/master --build 3 --display-last 10

v0.0.1
```
