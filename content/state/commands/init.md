---
title: "Command: init"
---

The `init` command enables you to create a new empty project on your local machine. Once the project is created locally, use the `push` command to push your local changes to the ActiveState Platform so that you project is available in the Dashboard and to enable all project features, such as secrets.

## Usage

```text
state init <owner>/<project_name> <Language[@version]> [--path <path>]
```  

The "owner" argument is your username or the organization name that the project belongs to.

Use the `Language` argument to specify the language distribution the project should use. You must specify one of the following:

* perl
* python3
* python2

You can also optionally specify the version to use by appending `@version` to the language with the specific version number you want to use. If you don't specify a version, the latest available version for that language will be used.

Use the `--path` flag to specify the local directory where the project will be created.

## Example

You can use the state init command followed by the state push command to create a new project on the ActiveState Platform.

```text
state init jsmith/johnspython3.6 python3@3.6.6 --path C:\state_projects\mypython
cd C:\state_projects\mypython
state push
```

## Related Information

[push Command](/state/commands/push)