git-foreach
===========


Purpose
-------

**git-foreach** is a script performing ``git`` commands on a number of
repositories and, thus, allowing for a more flexible management of
multiple repositories. The script works by finding all repositories
below the current working directory and invoking the supplied command
there. By default, if no custom command is specified, each repository's
status will be displayed.


Usage
-----

A sample invocation can look like this:

```
$ git foreach
/dir/repo3
 M modified-file.py
/repo2
D  deleted-file.asm
/repo1
A  newly-added-file.c
```

Installation
------------

Being a simple shell script, installation is straight forward: The script needs
to be made executable and included in the command search path (in general
represented by the ``PATH`` variable).

Due to the script's name, ``git`` will recognize the command as well, so it can
be invoked as ``git foreach`` but also via ``git-foreach``.
