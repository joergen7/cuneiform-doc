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
:ref:`Example e-1.5 <e-1-5>`, when written with explicit type information, looks
like this:

Example e-2.1::
        
    deftask add( c( String ) : a( String ) b( String ) )in perl *{
      $c = $a+$b
    }*
    
Cuneiform's type system is rudimentary compared to the type systems you may know
from other languages. In fact, Cuneiform possesses only two types:

- String
- File

In the following section, we have a closer look at how to work with files.

Using Files
^^^^^^^^^^^

We can mark a task parameter to be a file by attaching the `File` type to the
parameter. A simple task using files may be a task outputing a single file with
the content `"Hello world"`

Example e-2.2::
        
    deftask hello( out( File ) : person )in bash *{
      echo "Hello $person" > $out
    }*
    
    hello( person: "world" ); 
        
The task `hello` has one output parameter `out` of type `File` and one input
parameter `person` having the default type `String`. Calling this task with the
argument `"world"` returns a file with the content `"Hello world"`. Entering the
above example in the Cuneiform interactive shell should look like this::
        
        
    > hello( person: "world" ); 
    INFO  Query 73f90ac7-8707-4e60-847c-37376a1bc9b4 started.
    INFO  Query 73f90ac7-8707-4e60-847c-37376a1bc9b4 finished: '5532951210_1_out'


Another example task in which we concatenate two files:

.. _e-2-3:

Example e-2.3::
        
    deftask cat2( out( File ) : a( File ) b( File ) )in bash *{
      cat $a $b > $out
    }*
    
    cat2( a: hello( "Maria" ) b: hello( "Oliver" ) );
    
The task `cat2` has one output parameter `out` and two input parameters `a` and
`b` all of type `File`.


Mapping Over Lists
^^^^^^^^^^^^^^^^^^


Processing Lists as a Whole
^^^^^^^^^^^^^^^^^^^^^^^^^^^


Assignments
-----------

Assignment a-2.1
^^^^^^^^^^^^^^^^

Consider the variables `a` and `b` defined as follows::
    
    deftask to-file( out( File ) : str )in bash *{
      echo $str > $out
    }*
        
    a = to-file( str: "Bob" "Martha" "Eva" );
    b = to-file( str: "Geldorf" "Stuart" "Green" );

What happens if we call the task `cat2` defined in :ref:`Example e-2.3 <e-2-3>` for the
two lists `a` and `b` like this::
        
    cat2( a: a, b: b );
    
What is the size of the output list? What is the content of the output files?
Verify your answer in the Cuneiform interactive shell.
