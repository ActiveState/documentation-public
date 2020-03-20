---
title: "Command: secrets"
---

The `secrets` command allows a user to manage their secrets within a Project. For more information on secrets, what they represent and how they fit into the wider picture of the State Tool and the Platform check out [Getting Started](start.html).

## Usage

```text
state secrets 
state secrets set <secret-namespace> <secret-value>
state secrets get <secret-namespace>
state secrets sync
```

### state secrets

Lists available secrets for the current project.

### state secrets set

Sets the value for the given secret.

 - `<secret-namespace>` the namespace is in the format of `<scope>.<name>`, where `<scope>` is one of `user` or `project` and `name` is the name of the secret.
 - `secret-value` the value that you want to assign to this secret

### state secrets get

Retrieves the value for the given secret.

 - `secret-namespace` the namespace is in the format of `<scope>.<name>`, where `<scope>` is one of `user` or `project` and `name` is the name of the secret.

### state secrets sync

This will sync all secret values that you have access to with project members that should also have access to these secrets. This is mainly intended for when new members join a project.

### Related Information

- [Secrets](start.html#secrets)

