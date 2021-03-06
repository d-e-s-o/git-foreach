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

In order for batch operations to be able to reference the repository a
command is invoked in, **git-foreach** provides a special variable,
``REPO``. The variable contains the name of the very repository the
command is invoked in (i.e., the name of the directory the repository is
contained in).

An example incorporating this variable looks as follows:

```
$ git foreach remote add github 'git@github.com:d-e-s-o/${REPO}.git'
$ git foreach remote -v
/dir/repo3
github  git@github.com:d-e-s-o/repo3.git (fetch)
github  git@github.com:d-e-s-o/repo3.git (push)
/repo2
github  git@github.com:d-e-s-o/repo2.git (fetch)
github  git@github.com:d-e-s-o/repo2.git (push)
/repo1
github  git@github.com:d-e-s-o/repo1.git (fetch)
github  git@github.com:d-e-s-o/repo1.git (push)
```

It is important to properly escape the variable reference in order to
avoid any substitution by the currently running shell. In the example
above, the correct behavior is achieved by putting the string containing
the variable reference in single quotes.

In case one is unsure about the proper escaping or just wants to double
check the to-be-invoked command, the -n/--dry-run option can be used:

```
$ git foreach --dry-run remote add github 'git@github.com:d-e-s-o/${REPO}.git'
./dir/repo3
git remote add github git@github.com:d-e-s-o/repo3.git
./repo2
git remote add github git@github.com:d-e-s-o/repo2.git
./repo1
git remote add github git@github.com:d-e-s-o/repo1.git
```

Using this option, the command that is about to be executed is shown for every
repository. No action aside from that is actually performed.

As was apparent from the examples shown so far, **git-foreach** by default
prints the directory an action is performed (or is to be performed) in before
the result of the command is displayed. Using the -q/--quiet option, the script
can be silenced:

```
git foreach --dry-run --quiet remote add github 'git@github.com:d-e-s-o/${REPO}.git'
git remote add github git@github.com:d-e-s-o/repo3.git
git remote add github git@github.com:d-e-s-o/repo2.git
git remote add github git@github.com:d-e-s-o/repo1.git
```

If you want to pass additional command line options to the ``git`` command to
run in each repository, you should separate the command along with its options
so that those options are not interpreted by **git-foreach**. E.g.,

```git foreach -- diff -U10```


Installation
------------

Being a simple shell script, installation is straight forward: The script needs
to be made executable and included in the command search path (in general
represented by the ``PATH`` variable).

Due to the script's name, ``git`` will recognize the command as well, so it can
be invoked as ``git foreach`` but also via ``git-foreach``.
