---
title: auth
---

Authenticate your account on the ActiveState Platform.<!--more-->

## Usage

To authorize your account:

```text
state auth [--username <value>] [--password <value>] [--token <value>]
```

To sign out from the Platform:

```text
state auth logout
```

To start the sign up process on the command line:

```text
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
