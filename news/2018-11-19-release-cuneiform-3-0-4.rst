Release Cuneiform 3.0.4
=======================

2018-11-19

I have released `Cuneiform 3.0.4 <https://github.com/joergen7/cuneiform/releases/tag/3.0.4>`_. This release brings performance improvements to the Cuneiform interpreter. This means that much larger programs can be evaluated. Also, more type annotations have been added to the language, making more explicit the in-going and out-going types of iteration expressions. Moreover, it adds Elixir foreign language support.

Compatibility
-------------

* All Cuneiform components are now compatible with OTP-21.x

Language Syntax
---------------

* In a for-iteration the list(s) iterated over must now have a type annotation.
* In a fold-iteration both the accumulator and the list iterated over must now have a type annotation.

Foreign Language Support
------------------------

* Elixir foreign language support added.

Syntax and Type Checking
------------------------

* The type checker now checks the type of the first argument of a fixpointed function.
* Binding the same name twice in a for-iteration now results in a parse error.

Interpreter
-----------

* A bug has been fixed which caused the interpreter to apply an operation although one of its operands is a user-error.
* A bug has been fixed which caused the interpreter to ignore a user-error if it was the cons-head of a list.
* The interpreter now runs a machine similar to a CEK-machine. This has the effect that interpreter substitutes variables as late as possible and that it sends foreign function applications to the CRE in bulk. These changes improve performance.
* Each time the interpreter receives a foreign function application result it now waits 250 ms for more results to come in. This way, it can substitute futures for results in bulk instead of one at a time. This change improves performance.

Execution Environment
---------------------

* Killing the CRE now also kills the Cuneiform client instead of leaving it a zombie process.

Logs
----

* The common runtime environment now serves the foreign function application history under `/history.json` (instead of `/cache.json`).
* In the application history, the root field is now called `history` (instead of `cache`).
* In the application history, the `stat` field is now a child of the `result` field (instead of the `delta` field).