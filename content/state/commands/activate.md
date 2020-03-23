---
title: "activate"
---

Activate an ActiveState Platform project on your local computer.<!--more--> Activating is the process of downloading the build associated with the project, which includes the language interpreter and the set of packages selected for the project, and creating a virtual environment for the interpreter to run in. 

For example, when you run `state activate ActiveState/ActivePython-3.6`, ActivePython 3.6 and all selected packages are installed and configured, and a virtual environment is created. This allows you to run code in the project directory using your specific project configuration. 

If you have system or other installed versions of Python on the computer they are not affected by the activated project, and the activated project is totally isolated from any existing Python configuration. This ensures that you are working with a clean environment that will not be affected by dependencies in other projects. 

## Usage

```text
state activate [--path <path>]
state activate <owner/projectName> [--path <path>]
```

Use the `path` flag to specify the directory to activate the project in, so you are not prompted to choose the default location or enter a different directory.

### state activate

You can run `state activate` without any arguments if you are inside a directory that has an `activestate.yaml` configuration file in its parent directory structure. This will activate that `activatestate.yaml`.

### state activate <owner/projectName>

This will activate a project for the first time, or from a directory other than the project directory.

The "owner" argument is your username or the organization name that the project belongs to.
