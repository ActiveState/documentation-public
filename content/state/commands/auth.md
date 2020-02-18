---
title: "auth"
---

The `auth` command allows you to authenticate your account on the ActiveState Platform.

## Usage

```text
state auth [--username <value>] [--password <value>] [--token <value>]
state auth logout
state auth signup
```

### state auth

If no username, password or token is provided you will be prompted for your ActiveState Platform username and password. 

- `--username <value>`: Manually provide a username.
- `--password <value>`: Manually provide a password.
- `--token <value>`: Manually provide a token (this cannot be used with `--username`)

### state auth logout

Logs you out.

### state auth signup

You can use the signup argument to sign up for an account on the ActiveState Platform. You will be prompted for a username and password, your full name, and your email address. Your account will have limited access to the ActiveState Platform until you click the link in the confirmation email sent from the Platform to validate your email address.