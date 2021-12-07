# Best practices for python backend development

## Python best practices

I can recommend this best practices guide for general python programming:
https://gist.github.com/sloria/7001839

## How to design a good REST API

A good summary of best practices when designing a REST API is documented here: 
https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/

## Nuggets

Here are a few points I've learned from the past or just some not super obvious stuff that I find
extremely useful.

### Write a config file

It's always a good idea to create a config file that contains information like:

- Auth Credentials (e.g. for mail)
- Secrets (e.g. for token creation)
- Environment dependent parameters (e.g., host)
- URIs to other APIs (e.g. your database URI, some third party APIs you query)
- Some important flags (e.g. `enableBlacklisting`)
- ...

This has a lot of benefits:

- You don't commit vulnerable information (like passwords) but only fill out those parts of the config file after deployment. And you don't need to change some actual code so there won't be any merge conflicts when pulling a new version.

### Use a package manager

Pipenv can be seen as the npm for Python. It makes package management via pip easier (no more `requirements.txt`) and
handles virtual environments for you. [Read more...](https://pipenv.pypa.io/en/latest/)

### Use libraries

Of cause you won't build a complete webserver from scratch using only python standard libraries. Most probably you will always use flask. There are several good libraries that make your life even easier that build on top of flask.

A word on **Flask restx / Flask restless**: Takes away most of the marshalling work. But be careful: Depending on how sophisticated your app becomes, you will hit some limits pretty soon. As the marshalling is done automatically certain formats of the payloads and models are just not possible or require some ugly workarounds. 

The following libraries are my favourites for developing python backends:

- [Flask](https://flask.palletsprojects.com/en/2.0.x/): Microframework for web applications. I'm using it mainly for API specification and HTTP handling
- [Flask JWT Extended](https://flask-jwt-extended.readthedocs.io/en/stable/): For handling JSON Web Tokens. You will need this when you want to authenticate users.
- [Flask SQLAlchemy](https://flask-sqlalchemy.palletsprojects.com/en/2.x/): Integrates [SQLAlchemy](https://www.sqlalchemy.org/) into flask. The go-to ORM library for Flask apps. (For SQL databases)
- [Flask migrate](https://flask-migrate.readthedocs.io/en/latest/): Brings alembic migrations to SQLAlchemy.
- [Flask-Marshmallow](https://flask-marshmallow.readthedocs.io/en/latest/): For marshalling models.
- [Webargs](https://webargs.readthedocs.io/en/latest/): For parsing request payloads.
