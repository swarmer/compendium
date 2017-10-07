# Python packaging

The ecosystem related to building, downloading, installing and managing
Python packages has had a long rocky history and is still actively evolving. Here's a
rough overview of modern components used for packaging in python.


## Standard library
These projects are part of core CPython codebase and are released on the same schedule
as CPython itself.

- venv  
    A virtual environment creation tool, heavily inspired by virtualenv
- ensurepip  
    A standard package that allows to bootstrap pip into a python installation,
    allowing it to support third party package installation.
- distutils  
    A package that provides tools for describing and building python packages.
    Now superseded by setuptools (pip runs install scripts using setuptools
    even if they import distutils) and is mostly kept for backwards compatibility.


## PyPA

[PyPA](http://www.pypa.io/) (Python Packaing Authority) is a working group that
oversees the development of core packaging utilities and libraries for Python.

Below is a non-exclusive list of their projects.

- setuptools  
    The most widely used current package definition and management library.
    This is what you'll use to define and build your package today.

    Besides `setuptools`, this project contains another top-level package: `pkg_resources`.
    It provides utilities and classes that allow introspection of installed packages.
- pip  
    The most popular tool used to download and install python packages.
- virtualenv  
    Still very popular for creating virtual environments (and the only popular option
    for python 2).
- twine  
    A utility that was used to securely upload package archives to PyPI (although
    recent python versions now also use HTTPS). Also allows to upload pre-build and
    pre-tested archives, lowering the risk of putting out a broken release.
- wheel  
    `wheel` is a relatively recent binary format for distribution of prebuilt
    python packages. It allows to publish packages with all required supporting libraries
    already built and included instead of requiring package users to have a working compiler for them.

    The `wheel` package contains supporting utilities for this format.
- pipfile  
    A more functional alternative to `requirements.txt` files. It includes support
    for `Pipfile` files written in TOML that specify application dependencies with the
    ability to list development dependencies separately.

    The main feature is the ability to generate from inexact requirements
    a `Pipfile.lock` file that will contain exact versions of dependencies with
    which the application will presumably be tested to work well. Listing exact
    package versions facilitates reproducible functional builds.
- warehouse  
    The next version of package repository software that will in future replace the
    code that's currently powering PyPI.
- distlib  
    A new collection of lower-level utilities to be used by the packaging ecosystem.
    Among other things, contains implementations of some of the newer PEPs related to packaging,
    package introspection utilities and tools for accessing package indexes like PyPI.
- packaging  
    A small utility library that currently seems to contain utilities for working with,
    and parsing package versions or requirement strings.


## Third-party projects

- pipenv  
    A general python application management utility. Uses `pipfile` to specify
    and lock dependencies. Provides a single interface that calls out to other utilities
    such as virtualenv, pip, or safety.
- safety-db  
    A database containing known vulnerabilities in Python packages specified in a
    machine-readable way.

    `safety` is a companion tool that checks dependencies using safety-db.
- conda  
    A separate package manager used in the anaconda scientific python distribution.
    Provides a lot of easy to install prebuilt scientific packages.
    Cannot install normal python packages, but can install `pip`, allowing them
    to coexist in one environment.
