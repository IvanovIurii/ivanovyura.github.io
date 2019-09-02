---
layout: post
title: First look at Poetry
author: Iurii Ivanov
tags: [poetry, pyenv]
---

**Here is how to and some thoughts about Poetry.**

Poetry does not allow you to create virtual environment with specific python version, so you use `pyenv` first, to specify your local python version, then you can set up its environment.

```bash
pyenv install 3.7.1
pyenv local 3.7.1
poetry install
```

After `poetry install` command, new virtual environment should be created, the same for `add` command.
