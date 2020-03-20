---
title: State Tool
aliases:
    - /start/state.html
---

## Introducing the State Tool (Beta)

Wouldn’t it be great if any developer could run a single command and immediately get started contributing code to your project? And wouldn't it be even better to automate all of the tedious configuration workflow you usually go through? This is exactly what ActiveState is working to facilitate with our State Tool. 

Once you have set up your runtime environment, by creating a Project on the ActiveState Platform and are getting successful builds, you can instantly deploy your runtime environment locally using the State Tool. The State Tool creates a virtual environment, similar to `virtualenv` and `pipenv`, and will not contaminate any of the preexisting Python installations or environments you have configured.

## About the State Tool

The State Tool is the command line tool for the ActiveState Platform. It allows you to manage and use Platform projects right from the command prompt. You can create new projects, view existing projects, and download and install project runtimes.

The State Tool has two distinct capabilities:

* **Commands**: These are for tasks you want the State Tool to do. You can enter commands and subcommands using state [command] on the command line. 
* **Flags**: These are for providing optional parameters to modify the behavior of commands. Flags are specific to the command and each command can have its own flags. For example, `--language python3` in the `state init` command causes Python 3 to be selected as the runtime language.

You can learn the State Tool command line interactively using the `--help` flag. Help is provided for each command and subcommand, and you can explore the hierarchy of commands until you find what you need.

For example, the following commands provide increasing detail about the `state secretes set` subcommand:

```
# list information about the available commands
state --help

# show details for the secrets command
state secrets --help

# show details for the set subcommand
state secrets set --help
```


## Installing the State Tool

**Note**: Currently, the State Tool is supported for ActivePython and ActivePerl projects on Linux and Windows. Upcoming releases will support macOS and additional languages.

### Installation on Linux

You should have `curl` installed before you can run the script to install the State Tool. Alternatively, you can manually download and run the `install.sh` file.

1. Open your command prompt and enter the following command on one line:

    ```text
    sh <(curl -q https://platform.activestate.com/dl/cli/install.sh)
    ```
    The latest version of the State Tool will be downloaded, verified, and installed.

### Installation on Windows

**Important**: The State Tool installation requires PowerShell version 3.0 or higher. On older versions of Windows you will need to manually upgrade PowerShell to a supported version before completing the installation. For more information, see [Upgrading existing Windows PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-windows-powershell?view=powershell-7#upgrading-existing-windows-powershell).

1. Start PowerShell as an Administrator. Click the **Start** menu, search for **Windows PowerShell**, right click it and select **Run as Administrator**.
2. At the prompt, enter the following command:
    
    ```text
    IEX(New-Object Net.WebClient).downloadString('https://platform.activestate.com/dl/cli/install.ps1')
    ```
    
    The latest version of the State Tool will be downloaded, verified, and installed.
3. Start your command prompt (`cmd.exe`) to use the State Tool. Click the Start menu, search for Command Prompt, and click the menu item.

**Important**: Currently, you cannot run the State Tool in PowerShell. You must use the command prompt (`cmd.exe`). Support for PowerShell is coming soon.

## Usage

The basic usage for setting up a local virtual environment with your project is: 

```text
$ state activate owner/projectName
```

Where "owner" refers to your username or the organization name that the project belongs to.

### Working with your activated project

There are two ways to reactivate an existing project:

- Enter `state activate owner/projectName` anywhere on your system and you will be given the option to reuse your previously used directory and enter into an activated state.
- Open your terminal and navigate to the directory that contains the `activestate.yaml` file for the project  and enter `state activate` without any additional arguments.

To verify that your environment is "activated":

- When in an activated state the “ACTIVESTATE_ACTIVATED” environment variable will be defined. Also if your terminal shell allows for it, an informational message starting with **Active State:** will be printed after each command is executed. On Linux, you can check the value of the environment variable by entering the following command:

```text
printenv | grep ACTIVESTATE_ACTIVATED
```

### Using Your Project

Whenever you are in an “activated state”, your shell will be configured to use the runtime environment you created on the ActiveState Platform. Any preexisting Python installations you have will be overridden ONLY while using the “activated state”.

The State Tool provides a number of ways to configure your ActiveState Platform project to integrate it with your development environment. You can customize your configuration by editing the `activestate.yaml` configuration file in your project's root directory.

You can use the following mechanisms to customize the configuration of your  project: 

- **Constants**: Define constant values that can be reused throughout your configuration file. For example, you can define a hostname that's used repeatedly as a constant and then use the constant name for subsequent references.
- **Secrets**: Securely save and retrieve sensitive values for use in your configuration file, either at the project or user level. 
- **Scripts**: Name and define scripts that you can run within your project by typing the name of the script. 
- **Events**: Run scripts or commands when particular State Tool events occur. For example, you can hook into the State Tool ACTIVATE event to start up the database server for your development environment.

For more detailed information and examples, see [Getting Started](/state/start.html). 

## Command Reference

This release of the State Tool includes a number of commands for interacting with the ActiveState Platform and your projects. For the complete list run `state help`, or run `state <command_name> help` for help with a particular command.

- [activate](activate.html)
- [auth](auth.html)
- [clean](clean.html)
- [events](events.html)
- [export](export.html)
- [fork](fork.html)
- [history](history.html)
- [init](init.html)
- [languages](languages.html)
- [organizations](organizations.html)
- [packages](packages.html)
- [platforms](platforms.html)
- [projects](projects.html)
- [pull](pull.html)
- [push](push.html)
- [run](run.html)
- [scripts](scripts.html)
- [secrets](secrets.html)
- [show](show.html)
- [update](update.html)

## Logging and configuration

### Linux

On Linux the State Tool logs and configuration files are located in `~/.config/activestate/cli-unstable`.

The log file is named `log.txt`.

The configuration file is named `config.yaml`. The configuration file stores the API token used to authenticate with the ActiveState Platform and your default locale. You can change the default location by creating an ACTIVESTATE_CLI_CONFIGDIR environment variable and setting the location to use.

The language runtimes used by your activated projects are stored in subfolders under `~/.cache/activestate/`. You can change the default location by creating an ACTIVESTATE_CLI_CACHEDIR environment variable and setting the location to use.

### Windows

On Windows, the State Tool logs and configuration files are located in

The State Tool logs and configuration files are located in `C:\Users\<User>\AppData\Roaming\activestate\cli-unstable\`

The language runtimes used by your activated projects are stored in subfolders under `%HOME%\AppData\Local\activestate\cli-unstable\`. You can change the default location by creating an ACTIVESTATE_CLI_CACHEDIR environment variable and setting the location to use.


## Uninstalling the State Tool

You can uninstall the State Tool by running the `state clean` command. For more information, see the [command reference](/state/clean.html).