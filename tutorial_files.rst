Files and Lists
===============

Learning Objective
  This tutorial teaches you to pass and return files from Cuneiform
  tasks. Additionally, it introduces lists and  how to apply tasks to
  lists.
  
  
Difficulty
  Basic
  
Duration
  30 min
  
Prerequisites
  Basic experience with Cuneiform (see :ref:`tutorial_basics`).
  
  
Introduction
------------




Explanation and Examples
------------------------

In the :ref:`tutorial_basics` tutorial you have learned how to define and call
tasks. You may have noted that neither the input parameters nor the outputs had
any type information attached. In fact, there is a default type: `String`, which
is assumed when no further type information is given. Our `add` task in
:ref:`Example e-1.5 <e-1-5>`, when written with explicit type information, looks like this

Example e-2.1::
        
    deftask add( c( String ) : a( String ) b( String ) )in perl *{
      $c = $a+$b
    }*
    
Cuneiform's type system is rudimentary compared to the type systems you may know
from different languages. In fact, Cuneiform possesses only two types:

- String
- File

In the following section, we have a closer look at how to work with files.

Using Files
^^^^^^^^^^^


Mapping Over Lists
^^^^^^^^^^^^^^^^^^


Processing Lists as a Whole
^^^^^^^^^^^^^^^^^^^^^^^^^^^


Assignments
-----------

Assignment a-2.1
^^^^^^^^^^^^^^^^
