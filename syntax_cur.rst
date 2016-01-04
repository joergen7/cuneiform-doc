.. _syntax_cur:

Curry Expression (cur)
======================

A Curry Expression (cur) simplifies a Task Definition by binding one or more
of its parameters. It starts with the keyword ``curry`` and binds the special parameter
``task`` to a :ref:`syntax_compoundexpr` of Task Definitions. Then follow parameter
bindings.

A :ref:`syntax_expr` can be a Curry Expression.

**app:**

.. image:: img/cur.png

::

    cur ::= 'curry' '(' 'task' ':' compoundexpr ( ',' binding )+ ')'
    
References:

- :ref:`syntax_compoundexpr`
- :ref:`syntax_binding`

ID:
   An ID is a regular string beginning with a letter and containing letters,
   numbers, or the symbols -, _, +, \*, or / and not being a keyword.


