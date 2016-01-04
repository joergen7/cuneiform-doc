.. _syntax_cond:

Conditional (cond)
==================

A Conditional (cond) has a clause :ref:`syntax_compoundexpr`, a then Compound
Expression, and an else Compound Expression. If the clause evaluates to *nil*,
the Conditional evaluates to the else Compound Expression. Otherwise it
evaluates to the then Compound Expression.

A :ref:`syntax_expr` can be a Conditional.

**cond:**

.. image:: img/cond.png

::

    cond ::= 'if' compoundexpr 'then' compoundexpr 'else' compoundexpr 'end'
    
References:

- :ref:`syntax_compoundexpr`

Examples
--------

A Conditional evaluating to the string *"blub"*::
	
    if nil then "bla" else "blub" end
    
A Conditional checking if an ID *x* has converged returning it if true and
improving it if *nil*::
	
    if has-converged( state: x )
    then
      x
    else
      improve( state: x )
    end
