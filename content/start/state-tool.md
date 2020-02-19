---
title: "State Tool CLI"
weight: 4
---

The State Tool is the command line interface for the ActiveState Platform. This quick start is for intermediate or advanced developers who want to get up and running right away.<!--more-->

### Install the State Tool

On Linux:

```text
sh <(curl -q https://platform.activestate.com/dl/cli/install.sh)
```

On Windows:

1. Run the following as Administrator in PowerShell:

    ```text
    IEX(New-Object Net.WebClient).downloadString('https://platform.activestate.com/dl/cli/install.ps1')
    ```

2. Start the command prompt (`cmd.exe`) to use the State Tool.

### Sign in to the ActiveState Platform

If you don't have a Platform account yet, you need to sign up:

```text
state auth signup 
```

Enter the requested information at the prompt to register your account. You will receive an email to verify your account. You have limited permissions to the Platform before you verify it. After registering your account you can sign in.

If you already have an ActiveState Platform account, or you just created an account you need to sign in:

```text
state auth
```

Enter your username and password for the Platform at the prompts.

### Create a new project locally

```text
state init <username_or_org_name>/<project_name> --language python3
```

### Change directories into your project folder 

Linux:

```text
cd <username_or_org_name>/<project_name>
```

Windows:

```text
cd <username_or_org_name>\<project_name>
```

### Push your project to the ActiveState Platform

```text
state push
```

### Add required packages for your project 

```text
state packages add requests@2.21.0

state packages add pandas
```

### Synchronize your local project with the Platform project

```text
state pull
```

### Activate your project

```text
state activate
```

### Access documentation for CLI commands

To learn more about the State Tool commands, run `state --help` in the terminal.

For help on individual commands, run `state COMMAND --help`. For example, `state packages --help`.

For more information on the State Tool and the available commands see the [State Tool section](/state/).