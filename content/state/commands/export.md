---
title: "Command: export"
---

The `export` command allows you to export the contents of the JSON Web Token (JWT) you are using to authenticate with the Platform, or the build recipe (the set of packages and operating system settings) used by your project.

## Usage 

To print your JWT credentials:

```text
state export jwt
```

To print a JSON formatted recipe: 

```text
state export recipe
```

To print the recipe for a particular commit:

```text
state export recipe <commitID>
```

You must run the `state export` command from the directory for the Platform project you want to export the build recipe for.
