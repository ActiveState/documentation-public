---
title: "update"
---

Updates the State Tool to the latest available version.

The `update` command allows you to download the latest release of the State Tool on demand. By default, the state tool checks for an updated version on a regular basis. 

You can disable automatic updates by running `state update` with the `--lock` flag. If you disable automatic updates you can force an update by manually running `state update`.

## Usage

```text
state update
state update --lock
```

### state update

Checks for a new version and updates the state tool.

### state update --lock

Turns off automatic updates for individual projects. The version will remain locked at current version for the project when the command runs. The State Tool will still update itself for other projects

When automatic updates are turned off you can still manually update by running the `state update` command.
