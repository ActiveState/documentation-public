---
title: "Command: platforms"
---

The `platforms` command lists the platforms in your project, and allows you to add and remove platforms, and search for available platforms on the ActiveState Platform. 



## Usage

To list the platforms in your project:

```text
state platforms
```

Search all of the platforms available on the ActiveState Platform:

```text
state platforms search
```

The output lists the Name (Windows, Linux, etc.), Version, and Bit Width for each Platform. Bit Width indicates whether the platform supports the 32-bit or 64-bit version of an operating system.

To add a platform:

```text
state platforms add [--bit-width 32|64] <platform> <version>
```

To remove a platform:

```text
state platforms remove [--bit-width 32|64] <platform> <version>
```


## Examples:

The output of `state platforms` is a list of configured platforms. Bit Width indicates whether the platform supports the 32-bit or 64-bit version of an operating system.

```text
Platforms:
 Name          Version            Bit Width
------------  -----------------  --------------
 Windows       10.0.17134.1       64
```

Add a Windows 10 platform:

```
state platforms add Windows 10.0.14393
```

Remove a Linux platform

```
state platforms remove Linux 
```