---
title: "Command: pull"
---

The `pull` command will update your `activestate.yaml` so that it references the latest version of your platform runtime environment. When you update the packages in your project on the Platform and successfully created a new build, you need to run the `pull` command to make the updated build available in your local environment.

When you state activate your project, and there is a newer commit available, you will be notified that you need to run the `pull` command to get the up-to-date version of your Platform project.

## Usage

```text
state pull
```