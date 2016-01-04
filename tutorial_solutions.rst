.. _tutorial_solutions:

Solutions
=========

Cuneiform Basics
----------------

Assignment a-1.1
^^^^^^^^^^^^^^^^

::

    deftask square( b : a )in perl *{
      $b = $a*$a;
    }*
    
    square( a: 5 );
    
Assignment a-1.2
^^^^^^^^^^^^^^^^

::

    deftask concat2( c : a b )in python *{
      c = a+b
    }*
    
    deftask concat3( c : a b )in bash *{
      c="$a$b"
    }*
    
    concat2( a: "bla", b: "blub" );
    concat3( a: "sha", b: "lala" );
        
    
Assignment a-1.3
^^^^^^^^^^^^^^^^

Given the following state::

    x = 5;
    y = x;
    
On updating the variable ``x = 6;`` the variable ``y`` implicitly also changes
its value. That is because the variable ``y`` does not hold the literal value
and is, therefore, independent from ``x`` but is a placeholder for the
expression ``x`` and will evaluate to whatever ``x`` is. In this Cuneiform's
Call-By-Name evaluation strategy differs from most general purpose programming
language which use a Call-By-Value evaluation strategy.



