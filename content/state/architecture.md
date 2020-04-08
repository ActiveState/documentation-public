---
title: About the State Tool architecture
---


## Installation

When you install the State Tool, you can accept the default location which will install the `state` executable in a folder on your PATH, or you can choose a custom location and the State Tool will prompt you add the directory to your PATH or you can add the directory to your PATH manually.

### Linux 

```text
.
├── .bash_history
├── .bash_logout
├── .bash_profile
├── .bashrc
├── .cache
├── .config
├── .local
    └── bin
       └── state           # The State Tool binary in the default install location  
                            # on Red Hat Enterprise Linux (RHEL 8).
```

## Authorization


### Linux 

```text
.
├── .bash_history
├── .bash_logout
├── .bash_profile
├── .bashrc
├── .cache
│   └── activestate           # Directory where virtual environments are created when you state activate a project.
├── .config
│   └── activestate           # Configuration files and logs for the State Tool.
│       └── cli-unstable
│           ├── config.yaml
│           ├── log.txt
│           ├── private.key
│           └── update-check
├── .local
    └── bin
        └── state

```

## Activation


```text
state activate ActiveState/ActivePython-3.6 --path /home/ec2-user/github/web-project-1
```

### Linux 

```text
.
├── .bash_history
├── .bash_logout
├── .bash_profile
├── .bashrc
├── .cache
│   └── activestate
│       └── bff70e45            # The ActiveState/ActivePython-3.6 virtual environment.
│           ├── bin             # This includes the python3 interpreter, supporting files
│           ├── doc             # and packages specified in the ActiveState Platform project
│           ├── include         # at https://platform.activestate.com/ActiveState/ActivePython-3.6
│           ├── lib
│           ├── licenses
│           ├── share
│           └── support
├── .config
│   └── activestate
│       └── cli-unstable
│           ├── config.yaml
│           ├── hail-update
│           ├── log.txt
│           ├── private.key      # A private key is created the first time you use
│           └── update-check     # the `state auth` command to authenticate with the ActiveState Platform.
├── github
│   └── web-project-1            # The location the ActiveState/ActivePython-3.6 project is checked out to
│       └── activestate.yaml     # Stores the reference to the ActiveState Platform project and project configuration.
├── .local
    └── bin
        └── state

```


### macOS

`tree ~/Library/Application\ Support/activestate/`

`tree ~/Library/Caches/activestate/`