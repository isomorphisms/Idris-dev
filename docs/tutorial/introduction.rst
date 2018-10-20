.. _sect-intro:

*****************************
Why dependent, static typing?
*****************************

Statically typed programming languages tell the compiler about your code rather
than leaving it to guess. For example, `C` wants to know if the 8 bits `01011011` (the 91st big-endian^[] byte value, which is more conveniently written in hexadecimal `[0-f]` as the hex code `x8a` (the 91st byte
value) are supposed to represent

- the integer 91 (which can be added)
- the ASCII character `[` (which cannot), 
- part of a longer [UTF-8](joel on software what every developer must know) character like [table],
- the Japanese JI5 character ス,
- part of a floating-point number or arbitrary-length integer,
- itself containing a bitcode for an address in memory (which, for example,
  shouldn’t be pointing outside the bounds the operating system gave to your
  program)
- the bits have some other meaning in a context like an MP3 file, UDP packet,
  streaming video, youtube WEBM video, H-264 encoded video, TIFF image, SVG
  vector graphics file, 




^[] Computer bytes have other important properties like width (64 bits wide vs 32 bits wide for
example) and endianness (whether you read bits from the “left” or “right” of a
CD/DVD, spinning drive, or whatever happens on flash media)


The designers of languages like Haskell realised that the necessary information
supplied by you as to whether `x8a` == `01011011` is a character or an integer
has further implications which a compiler can use to help you program better.

For example, if a small sub-part of your program involves concatenating two
strings—one `N` characters long and the other `M` characters long, the result
should be `N+M` characters long—and the compiler can help you make sure you
define things that way.

(If that example sounds trivial, wait until you have to deal with `iconv`, `wchar_t`, ニ
nm سشㄓ, possibly intermingling with ASCII, possibly changing in endianness or
read-left-to-right-ness—and allocate+deallocate the memory for these things by
hand for yourself! No, that’s right, you don’t want to—and we certainly haven’t
gotten to more structured formats like video or HTTP or FIX which, not at all
helpfully for you, `Maybe` could have [omitted](meanderful.blogspot.com/tricks)
`Empty` or default fields for their own efficiency reasons.)





Idris’ designer agreed with this and wanted to go a step further: make types
themselves mutable.      
.. This accomplishes XXXXX

Computable types means you can write a program that will figure out what sort of
thing it needs to work with, as well as working with that thing. For example if
you want to store global variables in a singleton mono..thingie, but you only
create the singleton mono..thingie ``if`` some conditions are satisfied, …………
you can just say that in natural Idris, rather than having to invent a horrible
language-hack workaround just to get your point across to the compiler.
``IF`` some condition, ``THEN`` x is a ``sphere``, and being a ``sphere``
implies various things. ``OTHERWISE`` x would be a ``box``, and a ``box`` has
other properties. …………

[[server example]]

Combine computable types with the compiler’s type inference, and you have
helpful language innovation. You will be able to both tell the computer how to
figure out what kind of thing you’ll be giving it when, AND it will be able to
give you useful hints based on that.


Old programming languages distinguished
between types and values. For example, in `Haskell
<http://www.haskell.org>`_, `Char` is a type and `'a'` is a value of type
`Char`. Types are immutable, not variable, in languages like `C` or `Haskell`. 

.. I still don’t get what the poitn is so I can’t make this shorter. The intro should be clearer and get to the point immediately.

In a language with dependent types, however, types are not so different from
other sorts of variable.  As first-class language constructs in Idris, types may be //so?
manipulated like any other value. The type of

Lists of length `n` containing only `a`’s
lists of a given length `n` [1]_, ``Vect n a``, where ``a`` is the element
type and ``n`` is the length of the list and can be an arbitrary term.


This is useful because you can give the compiler some type-level facts about
properties your functions and objects. Then the compiler can point out if how
you wrote your function/datatype turned out in implementation to not satisfy
some of the type-level facts you said it should.

For example, lists are parameterised by their length. So the concatenation of
two lists will have a length as well, and the compiler can know about this
dimensionality requirement from your type definition. Thus if your definition of
concatenation-of-lists ends up giving the wrong dimension, the compiler can flag
that problem for you right away (either a problem in your type definition or a
problem in your coding of the concatenation function) — and make you straighten
one or the other out, rather than leaving you open to an arcane and
hard-to-trace error that you find out about some other, more unpleasant, way.


When types can contain values, and where those values describe
properties, for example the length of a list, the type of a function
can begin to describe its own properties. Take for example the
concatenation of two lists. This operation has the property that the
resulting list's length is the sum of the lengths of the two input
lists. We can therefore give the following type to the ``app``
function, which concatenates vectors:

.. code-block:: idris

    app : Vect n a -> Vect m a -> Vect (n + m) a


    //belongs somewhere else
Idris is a compiled
language which aims to generate efficient executable code. It also has
a lightweight foreign function interface which allows easy interaction
with external ``C`` libraries.

Intended Audience
=================

This tutorial 
is aimed at readers already familiar with a functional language such
as `Haskell <http://www.haskell.org>`_ or `OCaml <http://ocaml.org>`_.
In particular, a certain amount of familiarity with Haskell syntax is  //pick
one… either they need it or they don’t
assumed. 

For a more in-depth introduction to Idris
covering interactive program development, with many more examples, see
`Type-Driven Development with Idris <https://www.manning.com/books/type-driven-development-with-idris>`_
by Edwin Brady, available from `Manning <https://www.manning.com>`_.

Example Code
============

Example code has been typed out correctly and verified to run and do as
expected. 
The examples in this tutorial can be found under
``samples``. It is, however, strongly recommended that you type
them in yourself. We think you’ll learn faster that way.

.. [1]
   Typically, and perhaps confusingly, referred to in the dependently
   typed programming literature as “vectors”
