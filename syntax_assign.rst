.. _syntax_assign:

Assignment (assign)
===================

An Assignment (assign) binds a :ref:`syntax_compoundexpr` to a
list of IDs. In the simplest case a Compound Expression is bound to one ID.

A :ref:`syntax_stat` can be an Assignment. Furthermore, an Assignment can be
part of the native body of a native :ref:`syntax_defun`.


**assign:**

.. image:: img/assign.png

::

    assign ::= ID+ '=' compoundexpr ';'
    
References:

- :ref:`syntax_compoundexpr`

ID:
   An ID is a regular string beginning with a letter and containing letters,
   numbers, or the symbols -, _, +, \*, or / and not being a keyword.

Examples
--------

Binding the integer literal *5* to the ID *x*::
	
    x = 5;
    
Binding the string literal *"Hello world"* to the ID *x*::
	
    x = "Hello world";
    
Binding the output of the task *greet* to the ID *out*::
	
    out = greet( person: "Jorgen" );
    
Binding the first output channel of the task *sim* to the ID *out1* and the
second output channel to the ID *out2*::
	
    out1 out2 = sim();
    
Binding a Conditional to the ID *x*::
	
    x = if predicate then "bla" else "blub" end;
