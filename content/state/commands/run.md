---
title: "run"
---

The `run` command allows you to manually run scripts you have defined for your projects by name. Script names are case-sensitive.

## Usage

```text
state run <script_name>
```

You can also pass arguments to your scripts, the same way you would to any command. Let's say you have a script called "hello" which takes an argument for who/what it is greeting, you could call it like this:

```text
state run hello world
```

Finally, if you are in an activated state (i.e. you've ran `state activate`) you don't need to use `state run` at all, you can run your scripts directly instead. So using the above "hello" example you could simply run

```text
hello world
```

## Related Information

- [Scripts](start.html#scripts)
- [scripts Command](scripts.html)