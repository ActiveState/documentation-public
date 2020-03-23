---
title: history
---

List the commit history for your project.<!--more--> It is limited to the past 10 commits.

This is the same as the information displayed in the **Project History** list in the **History** tab for your project on the ActiveState Platform.

## Usage

To view history for the current project:

```text
state history
```

To view history for a specified project by `<owner>/<projectname>`:

```text
state history --namespace ActiveState/ActivePython-3.6.6
```

## Example

The following information is displayed in the output for each commit.

```text
commit e3a9e215-ed72-4de5-9271-73870a33d08a

Author: jsmith

Date: 12 Mar 2020 18:27

Description: Added language: python 2.7.17



python 2.7.17 added
```