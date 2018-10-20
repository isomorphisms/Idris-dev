.. _sect-starting:

***************
Getting Started
***************

Prerequisites
=============


//is this no longer true?……

Before installing Idris, you will need to make sure you have all 
of the necessary libraries and tools. You will need:

- A fairly recent version of `GHC <https://www.haskell.org/ghc/>`_. The
  earliest version we currently test with is 7.10.3.

- The *GNU Multiple Precision Arithmetic Library* (GMP) is available  from MacPorts/Homebrew and all major Linux distributions.

Downloading and Installing
==========================

The easiest way to install Idris, if you have all of the
prerequisites, is to type:

::

    cabal update; cabal install idris

This will install the latest version released on Hackage, along with
any dependencies. If, however, you would like the most up to date
development version you can find it, as well as build instructions, on
GitHub at: https://github.com/idris-lang/Idris-dev.

If you haven't previously installed anything using Cabal, then Idris
may not be on your path. Should the Idris executable not be found
please ensure that you have added ``~/.cabal/bin`` to your ``$PATH``
environment variable. Mac OS X users may find they need to add
``~/Library/Haskell/bin`` instead, and Windows users will typically
find that Cabal installs programs in ``%HOME%\AppData\Roaming\cabal\bin``.

To check that installation has succeeded, and to write your first
Idris program, create a file called ``console_test.idr`` containing the
following text:

.. code-block:: idris

    module Main

    main : IO ()
    main = putStrLn "Idris appears to be working…"

If you are familiar with Haskell, it should be fairly clear what the
program is doing and how it works, but if not, we will explain the
details later. You can compile the program to an executable by
entering ``idris console_test.idr -o console_test`` at the shell prompt. This will
create an executable called ``console_test``, which you can run:

::

    $ idris console_test.idr -o console_test
    $ ./console_test
    Idris appears to be working…

Please note that the dollar sign ``$`` indicates the shell prompt! Don’t type
`$` out; the terminal (console_test) should print one (or perhaps another prompt
ending in `$`, `#`, or `%`) for you.


Some useful options to the Idris command are:

- ``-o prog`` to compile to an executable called ``prog``.

- ``--check`` type check the file and its dependencies without starting the interactive environment.

- ``--package pkg`` add package as dependency, e.g. ``--package contrib`` to make use of the contrib package.

- ``--help`` display usage summary and command line options.

The Interactive Environment
===========================

Typing ``idris 〔ENTER〕`` at the shell prompt starts up the interactive
environment. You should see something like the following:

.. literalinclude:: ../listing/idris-prompt-start.txt

This gives a ``ghci`` style interface which allows evaluation of, as
well as type checking of, expressions; theorem proving, compilation;
editing; and various other operations. The command ``:?`` gives a list
of supported commands.

Below, we see an example run in
which ``console_test.idr`` is loaded, the type of ``main`` is checked and
then the program is compiled to the executable ``console_test``. Type
checking a file, if successful, creates a *bytecode* version of the file
(in this case ``console_test.ibc``) to speed up loading in future. The
bytecode is regenerated if the source file changes.

.. _run1:
.. literalinclude:: ../listing/idris-prompt-helloworld.txt
