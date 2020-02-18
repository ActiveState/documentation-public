---
title: "packages"
---

The `packages` command allows you to manage the packages within an ActiveState Platform project. 

## Usage

```
state packages
state packages list

state packages add <name[@version]>
state packages update <name[@version]>
state packages remove <name>

state packages search <name>
```

### state packages list

List the packages and versions currently included in your project. 

**Note**: If you run `state packages` without additional arguments you will get the same output as `state packages list`. 

```text
-------------  ------------
 Name           Version    
-------------  ------------
 numpy                     

 pluggy         0.12.0     

 pytest         4.3.0      

 requests       2.21.0     
-------------  ------------
```

In the example output, specific versions have been specified for pluggy, pytest, and requests. No version was specified for numpy, so the latest version available on the Platform will be used each time the project is built. 

If you want to view the packages and versions for a particular commit, an earlier saved version of your project, you can specify the `--commit` flag. Currently, the commit IDs for a project are only available in the **History** tab for the Project in the Dashboard.

For example:

`state packages list --commit 17167a9b-40f0-4bdf-b3ec-b2755badeb50`


### state packages add

Add a specific package to your project by name. You can optionally specify a specific version to use.

**Examples**: 

```text
state packages add requests

state packages add requests@2.21.0
```

If you do not specify the package version, the latest version available on the ActiveState Platform will be used each time a new build is created. Specifying the version "pins" the package to that version until you change it on the Platform or using the `state packages update` subcommand. 

### state packages remove

Remove a specific package from your project by name.

**Example**: `state packages remove requests`

### state packages search

Search for available packages by name or partial string.

**Example**: `state packages search requests`

### state packages update

Update a package in your project by name. By default the package is updated to the latest available version, but you can optionally specify a specific version to use.

**Examples**: 

```text
state packages update requests

state packages update requests@2.21.0
```