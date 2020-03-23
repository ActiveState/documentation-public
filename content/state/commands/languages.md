---
title: languages
---

List the languages in your project, and allows you to update the specified languages.<!--more-->

{{% notice note %}}
In order to build your project successfully, only one language can be specified.
{{% /notice %}}

## Usage

To list the languages in your project:

```text
state languages
```

To update a language:

```text
state languages update <Language[@version]>
```

Use the `Language` argument to specify the language distribution the project should use. You must specify one of the following:

* perl
* python

You can also optionally specify the version to use by appending `@version` to the language with the specific version number you want to use. If you don't specify a version, the latest available version for that language will be used.

## Examples:

A project using Python 3.6.6 can be updated to version 3.8.1 using the following command.

```text
state languages update python@3.8.1
```

You could alternatively specify a Python 2 version:

```text
state languages update python@2.7.14
```

If you want to use the latest version available, omit the version:

```text
state languages update python
```
 
{{% notice note %}}
If you want the latest Python 2 version available, you need to specify the latest version using the `Language@version` syntax.
{{% /notice %}}
