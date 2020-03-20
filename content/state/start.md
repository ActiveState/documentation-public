---
title: "Getting Started"
---

The State Tool offers a number of methods for simplifying and securing your Project configuration and integrating it with your development environment. 

For information on installing the State Tool, see [installation guide](/state#installation).

## Creating Your First Project

The State Tool cannot do anything without a project, everything lives under your project.

You can create your project either via the State Tool itself via the [state init](/state/init.html) command or by going directly to the ActiveState Platform Dashboard and creating it there. Since you probably still need an account let’s go with the latter.

Head over to http://platform.activestate.com and create an account if you don’t already have one, otherwise just login.

Once logged in go ahead and create a new project. You will be asked for a platform and language for your project, simply use the most fitting answers. For more information on projects check out the [Projects documentation](/projects).

## Activating Your Project

It’s time to activate your project! Go ahead and switch back to your command prompt. Before we can do anything we need to make sure that we’re authenticated, to do this simply run the [state auth](auth.html) command:

```text
state auth
```

You will be prompted for your username and password, and if all goes well it should show a friendly “You have authenticated” message. 

Now we’re ready to activate our project. Run the [state activate](activate.html) command:

```text
state activate owner/projectName
```

The owner would be your username or if you created your project in an organization then instead of your username you can use the organization name.

This will create a new project folder under the current working directory containing an “activestate.yaml” file with some essentials. The State Tool will “activate” under this new project directory. This is a brand new project though and being in an “activated state” doesn’t mean much yet, so let’s deactivate by executing the `exit` command (or hit `Ctrl+D`).

Now when you want to work on your project again you can run the same `state activate owner/projectName` command again from anywhere and you’ll be entered into an activated state under your project directory. Alternatively you can manually enter into your project directory and run `state activate` without any other arguments.

## Configuring Your Projects “Activated State”

So we have the basics in place, now it’s time to actually put everything to good use. What’s the point of all this if it’s not actually doing anything but changing a directory? Think of it as moving into a brand new house that’s completely empty; now it’s time to decorate. 

## Constants

You can define constants in your `activestate.yaml` file and reuse them throughout the file. Constants are defined in a `constants` section using name/value pairs: 

```text
constants:
  - name: LOCATION
    value: World
```

You can use the constants you define in other constants, scripts, events, and other configuration fields. The following example defines the same LOCATION constant, and references it in the subsequent entry as `$constants.Location`. Constants are referenced this way wherever you use them in your `activestate.yaml` file.

```text
constants:
  - name: LOCATION
    value: World
  - name: HELLO
    value: Hello $constants.LOCATION
```

Using configuration values as variables it supported for many different fields, not just constants. You can also wrap your "variables" in brackets in case you're using them in more advanced scenario's where the variable parser might otherwise get confused, so for example you could use your constant like so:

```text
constants:
  - name: LOCATION
    value: World
  - name: HELLO
    value: Hello ${constants.LOCATION}
```

## Secrets

Constants are great if you just want to reuse certain values throughout your `activestate.yaml` file, but what if you want to store values that are sensitive, and which shouldn’t be stored in version control or in any plain text format? This is what “secrets” (or “state secrets”... get it?) are meant for; the State Tool has built into it a very useful secret management solution. You should store any database passwords, API keys, and other sensitive credentials your project needs access to as secrets.

A “secret” is similar to a constant, except that its value is securely stored on the ActiveState Platform. It is encrypted using RSA encryption in a manner that no one but you will ever be able to decrypt (unless you start sharing your password - which... don’t do that!). Not even ActiveState knows the true value of your secrets; we only store the encrypted value. Secrets also have the concept of sharing, meaning you can share a secret with the people on your project.

### Secret Definitions versus Secret Values

It's important to differentiate between a secret definition and a secret value. You can define a secret without it having a value assigned yet. When a secret is defined but it has no value then the user will be prompted for a value when the secret is being used.

### Secret Scopes

When talking about secrets we need to also talk about secret scopes. A scope describes who the secret value "belongs to". Currently we support two scopes, "user" and "project".

The "user" scope denotes a secret value as belonging to a user. This means that when you define a secret that is "user scoped" that every user will have to set their own value for this secret, to which only they have access.

The "project" scope denotes a secret value as belonging to everyone in the project. This means that when someone defines a secret value for such a secret that everyone in the project will get access to this value.

### Setting secrets

To define a secret you use the command line tool, not the `activestate.yaml`. This is because secrets live on the ActiveState Platform (in client-side encrypted format -- we do not have access to the real values) and not in your local configuration file. We'll want to use the [state secrets](secrets.html) command to define a new secret:

```text
state secrets set project.secret-name secret-value
```

This will create a secret named secret-name with the value secret-value that will be shared with everyone who has permissions for the project.

If, instead, you want to define a secret that only you have access to, you need to define a user secret by specifying `user.secret-name`:

```text
state secrets set user.secret-name secret-value
```

This will still define the secret for everyone on the project, but only you will have access to the value you've set. Anyone else that uses this secret will be prompted for their own value.

### Retrieving secrets

Now that we have a secret defined we can start using it. To view secrets that exist for your current project you can run the [state secrets](secrets.html) command. This will produce a concise list of secrets, their “scope” (user or project) as well as a usage example (what you would use to set or retrieve their value).

To retrieve the value of a secret run:

```text
state secrets get project.secret-name
```

This will retrieve the value for a secret called `secret-name` whose value is shared with everyone in the project.

### Using secrets

So we can set and retrieve secrets, what about using them in our config (activestate.yaml)? This is actually very simple, and similar to how you use constants. Let’s use our “HELLO” constant from before but this time instead of referencing a constant called “LOCATION” we’ll reference a secret with that name instead. This syntax would look as follows:

```text
constants:
 - name: HELLO
   value: Hello $secrets.user.LOCATION
 ```

What’s happening here is the `$secrets.` prefix indicates that we want to “expand” our identifier as a secret, and the `user.LOCATION` bits identify it as a secret named LOCATION stored under the user. This syntax is compatible with the output of the “Usage” column when running `state secrets` to list your secrets. You can copy and paste that value right after the `$secrets.` prefix in your `activestate.yaml` file.

It's important to note that you do not need to first define the `user.LOCATION` secret. If a secret does not yet exist you will instead be prompted for its value when you try to access it.

## Scripts

Scripts in the State Tool can be compared to scripts in NPM, or build targets in a Makefile. You define a script and can then run it whenever you need to. Let’s start with something simple:

```text
scripts:
 - name: hello
   value: echo Hello World
```

This will register a script with the alias “hello”. You can run this outside your “activated state” via the [state run](run.html) command by running `state run hello`, but once you state activate it becomes much simpler, you simply invoke it by running hello.

### Using Languages

The above script would run under whatever shell the current system defaults to, so Bash on Linux/macOS and Batch on Windows. This is problematic if you are working on a cross-platform project. Sure you could use [constraints](#constraining-scripts), but wouldn't it be easier if you could just use one single script for all platforms?

For this the State Tool supports languages. You can configure your project on the [ActiveState Platform](https://platform.activestate.com) to include a Python or Perl runtime, after which can define a script to use that language, for example:

```text
scripts:
  - name: hello
    language: python3
    value: print("Hello World")
```

The following `language` settings are supported:

| Language | Description |
|----|----| 
| bash | For scripts that use `bash` (Bourne again shell).|
| sh | For script that use `sh` (Bourne shell). |
| batch | For scripts that use `cmd.exe` on Windows. |
| perl | For scripts that use your Perl runtime environment. |
| python2 | For scripts that use your Python 2 runtime environment. |
| python3 | For scripts that use your Python 3 runtime environment. |

**Note**: Support for specifying Tcl as the script language is not yet available. 

See the section on [Constraining Scripts](#constraining-scripts) for information on limiting language to the appropriate operating system. For example, only running batch scripts on Microsoft Windows.

### Calling Scripts From Other Scripts

Calling one script from another is fairly straight forward, you can access scripts as "variables" the same as many other activestate.yaml structures. Let's let the code do the talking:

```text
scripts:
  - name: hello
    language: python3
    value: print("Hello World")
  - name: greeting
    language: python3
    value: |
      $scripts.hello
      print("How are you doing?")
```

When you execute `state run greeting` it will inject the value of the "hello" script into the "greeting" script. The resulting code that ends up being ran would look like this"

```python
print("Hello World")
print("How are you doing?")
```

#### Calling Scripts by Their Path

The above example can be problematic when you are running scripts in various languages. For example the following code would certainly fail:

```text
scripts:
  - name: hello
    language: python3
    value: print("Hello World")
  - name: greeting
    value: |
      $scripts.hello
      echo "How are you doing?"
```

Note that the "greeting" script does not have a language defined, this means it runs as either Bash or Batch depending on your platform. But the "hello" script is still Python code, which is being embedded in bash code, which will lead to some sort of syntax error.

You work around such an issue by calling the script by its file, rather than just embedding the code. To do this you can use the `path()` method that lives on all scripts. So the above code would become:

```text
scripts:
  - name: hello
    language: python3
    value: print("Hello World")
  - name: greeting
    value: |
      $scripts.hello.path()
      echo "How are you doing?"
```

Now the resulting script will look something like this:

```text
/tmp/7979234.script.py
echo "How are you doing?"
```

The file in question will have a shebang with our interpreter defined in it, so you don't need to worry about providing the interpreter unless you are on Windows, which doesn't support shebang. For cross-platform compatibility you could instead use:

```text
  - name: greeting
    value: |
      python3 $scripts.hello.path()
      echo "How are you doing?"
```

That way we're explicitly saying Python is the interpreter for this file.

### Using Constants & Secrets

Scripts can use constants too, so for example you could instead use the following value:

```text
value: echo $constants.HELLO
```

This also works for secrets, so instead of the above you could use `echo $secrets.user.HELLO`. It gets more interesting though, because in the `activestate.yaml` EVERYTHING is a “variable”, so you could create another command that references our first command:

```text
scripts:
 - name: log-hello
   value: $scripts.hello > /tmp/hello.txt
```

You can see how used wisely this can quickly become very powerful.

The main use-case for scripts is to kick off builds, run tests, etc. But the sky’s the limit.

### Script Arguments

Scripts support arguments too! Using the hello world sample again, you could define your script like so:

```text
scripts:
 - name: hello
   value: echo hello $1
```

Now you can run `hello world` or `hello planet` and it should print out the argument you passed.

### Constraining Scripts

You can constrain scripts to only run on certain platforms. If a language is not specified for the script, they will be run as either bash or batch scripts, depending on the shell that you run them from. This can be problematic because bash and batch are two very different languages, and you might have cross-platform requirements. You can add constraints to your script entries to ensure that the correct command runs based on the operating system identified at run time. For example:

```text
scripts:
 - name: env
   value: printenv
   constraints: 
       os: linux,macos
 - name: env
   value: set
   constraints: 
       os: windows
```

Now when you run `state run env` on Windows it will execute the windows constrained script, whereas when you run it on Linux or macOS it will run the script constrained to those platforms.

Constraints can also be negative, so if you would want to run a script on any platform except windows you could use `os: -windows`.

The possible values for the OS constraint are:

 - windows
 - macos
 - linux

These values can be given in a comma separate fashion, and include a minus character to exclude them (e.g. `-windows`).

## Events

OK so we have constants, secrets and scripts, but your project has some special needs. It might require certain services to be running, or for certain non-language-specific dependencies to be installed. For this you can hook into events, the most important event of which is the ACTIVATE event, as the name implies this event is triggered when you state activate.

**NOTE**: Currently, ACTIVATE is the only available event. Additional events will be added in future releases.

Events act mostly the same as scripts do, except that they aren’t manually invoked and instead run when their event triggers. For example we could have an ACTIVATE event that looks like this:

```text
events
 - name: ACTIVATE
   value: systemctl start my-service
```

This would start a service whenever we enter an “activated state”. It’s worth noting that the ACTIVATE event has a special use-case: it is invoked as part of your bashrc (or zshrc, or fishrc, or ..) meaning it can export environment variables, register bash aliases, etc.

### Sharing With Your Team

Now that you have your `activestate.yaml` configuration file set up you can share it with your team. You can do this however you prefer, but if your team is using version control we recommend checking in your `activestate.yaml` file. As we add new capabilities you can update your configuration in the `activestate.yaml` file and share these capabilities with your team.
