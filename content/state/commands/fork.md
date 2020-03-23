---
title: fork
---

Create a fork of an existing Platform project.<!--more--> A fork is a copy of a project that you can edit.

## Syntax

```text
state fork --name <project_name> --org <owner> ActiveState-Recipes/Core [--private]
```

The "owner" argument is your username or the organization name for your copy of the forked project. If you do not specify the `--org` flag, you will be prompted to select the owner, from the orgs you belong to, interactively at the command prompt.

The "project" argument is the name of the project for your copy of the forked project. If you don't specify the `--name` flag, the name of the forked project is used. 

If you belong to a organization on a paid tier, you can use the `--private` flag to fork the project as a private project.