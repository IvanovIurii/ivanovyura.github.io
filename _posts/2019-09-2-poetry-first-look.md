---
layout: post
title: First look at Poetry
author: Iurii Ivanov
tags: [poetry, pyenv]
---

Here is "how to" and some thoughts about Poetry.

For a long time I wanted to touch Poetry, and finally it happend. 
So, as usual it had some pluses and minuses. I can say Poetry has some nice features, but I like Pipenv more anyway, or maybe I am just old dinosaur (previously I relly liked `pip` + `virtualenv`). 

# HOW TO

1. Install it globally.

```bash
pip install poetry
```

2. Now you can create a new project:

```bash
poetry new <project_name>
```

You will see the file `pyproject.toml` is created. It is kind of similar to `Pipfile`, where you can specify your Python version and all dependencies.

**Plus**, if you are already have the project created, just run `poetry init` in the root of it.

# VIRUAL ENVIRONMENT 

Poetry does not allow you to create virtual environment with specific python version, so you use `pyenv` first, to specify your local python version, then you can set up its environment.

```bash
pyenv install 3.7.1
pyenv local 3.7.1
poetry install
```

After `poetry install` command, new virtual environment should be created, the same for `add` or `remove` command.

# FEATURES

The one which looks good, is to check dependencies you have.

```bash
poetry show --tree
```

You will get the output similar to this (there are `flask_restplus` and `psycopg2` installed):

```bash
flask-restplus 0.13.0 Fully featured framework for fast, easy and documented API development with Flask
├── aniso8601 >=0.82
├── flask >=0.8
│   ├── click >=5.1 
│   ├── itsdangerous >=0.24 
│   ├── jinja2 >=2.10.1 
│   │   └── markupsafe >=0.23 
│   └── werkzeug >=0.15 
├── jsonschema *
│   ├── attrs >=17.4.0 
│   ├── pyrsistent >=0.14.0 
│   │   └── six * 
│   ├── setuptools * 
│   └── six >=1.11.0 (circular dependency aborted here)
├── pytz *
└── six >=1.3.0
psycopg2 2.8.3 psycopg2 - Python-PostgreSQL Database Adapter
```
