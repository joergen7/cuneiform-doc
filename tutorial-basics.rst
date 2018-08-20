.. _tutorial_basics:

Cuneiform Basics
================

Learning Objective
  This tutorial introduces you to the basic Cuneiform language concepts. You use the Cuneiform interactive shell, to define foreign functions, bind variables and perform computations. We illustrate these concepts with simple examples showing string manipulation and arithmetic operations. Furthermore, you familiarize yourself with Cuneiform's Call-by-Name evaluation strategy.
      
Difficulty
  Basic
  
Duration
  30 min
  
Prerequisites
  Basic programming background. A working installation of Cuneiform (see
  :ref:`setup` section).
  

Introduction
------------

This tutorial is an introduction to the most important concepts of Cuneiform. This is binding an expression to a variable and defining and calling foreign functions. Completing this tutorial, enables you to specify complex workflows and drive APIs in foreign languages like Perl, R, Python, and Bash.
      
Explanation and Examples
------------------------
  
Statements
^^^^^^^^^^

Statements are the building blocks of a Cuneiform
:ref:`syntax-script`. In addition to import-statements, there are 2 kinds of Statements: (i) definition-statements like variable bindings or function definitions and (ii) query-statements, performing computation. This section gives a quick overview about statements:

:ref:`syntax-let-define`
    Let definitions bind expressions to variables.

:ref:`syntax-fun-define`
    Function definitions introduce functions.

:ref:`syntax-query`
    Queries tell the interpreter which values you are interested in. Only computation steps actually contributing to are query are executed.


Unless specifying very simple workflows, we have to use these statements.

Let Definitions
^^^^^^^^^^^^^^^

Let definitions are used to bind an expression to a variable. Variables are placeholders for expressions which can be queried (see `Queries`_) or for intermediate results to be referenced in other parts of a script. Here we show how to use let definitions to bind literal expressions to a variable.

First, start the Cuneiform interactive shell by entering on the command line::

    cuneiform
  
.. hint::
   You can exit the Cuneiform interactive shell by entering ``quit``.
   
If you have not yet installed Cuneiform, please refer to the :ref:`setup`
section.
  
A let definition binds an expression to a variable. The statement is started by the ``let`` keyword and the variable name and its type appear on the left-hand side of an equals symbol while the expression to be bound appears on the right-hand side.

Example e-1.1::
	
    let x : Str = "5";
    
In this example we have bound the string literal ``"5"`` to the variable ``x``.
Let's look at another example.

Example e-1.2::

    let person : Str = "Peter";
    
Here, the expression is the string literal ``"Peter"`` and the bound variable is
``person``. A let statement tells the Cuneiform interpreter that whenever it
sees a variable like ``x`` or ``person`` the interpreter should replace that
variable with whatever expression is bound to it.

Cuneiform's type system checks at compile-time, whether an expression matches the declared type. Also, it prevents the use of unbound variables. So, whenever you use a variable, you can be sure that it is bound and has the right type, otherwise the compiler will tell you upfront.

This also means that order plays an important role: Since you can only use bound variables, a variable definition must precede its use. For example, the following pair of definitions is valid

Example e-1.3::

    let y : Bool = true;
    let z : Bool = not y;

However, introducing ``z`` before ``y`` would result in an error reporting that ``y`` is unbound.

It is possible to bind expressions that are more complex than string literals or Boolean expressions. But no matter how complex, a binding never triggers computation. It just binds an (unevaluated) expression to a variable. The reason is the way Cuneiform implements the Call-By-Name evaluation strategy.


Definition History
^^^^^^^^^^^^^^^^^^

To get an overview over the variables bound so far you can use the ``hist`` command.::
	
    > hist
    let x : Str =
      "5";

    let person : Str =
      "Peter";

    let y : Bool =
      true;

    let z : Bool =
      not y;

The ``hist`` command is not really a part of the Cuneiform language. It is rather a special signal that the Cuneiform shell understands and handles separately. Another such command is ``quit`` which terminates the Cuneiform shell.

Note that ``z`` is bound to the expression ``not y`` instead of ``false``. As we said earlier, let definitions do not trigger computations. So the expression ``not y`` is bound as is.


Queries
^^^^^^^

Let- and function definitions bind expressions to variables but do not trigger any computation. In contrast, a query-statement tells the interpreter which of the previously defined expressions we want evaluated. Queries are the only kind of statement, that actually trigger a computation. A query has the form of an expression terminated with a semicolon. To find out the value of the variable ``person`` we can query it.

Example e-1.4::

    person;
    
Assuming you have also entered Example e-1.2, you should get an output like this
on the Cuneiform interactive shell::

    > person;
    "Peter"
    : Str


Records and Record Types
^^^^^^^^^^^^^^^^^^^^^^^^

Records are compound data structures that associate a name with an expression. C and Scheme users may know records as structs. In Cuneiform, records are constructed using angle brackets.

Example e-1.5::

    <a = "bloob", b = false>

The above record associates the string ``"bloob"`` to the field ``a`` and the Boolean ``false`` to the field ``b``. Entering the expression as a query in the Cuneiform shell makes the shell echo the expression together with its type.::

    > <a = "bloob", b = false>;
    <a = "bloob", b = false>
    : <a : Str, b : Bool>

Record types also take the form of angle-bracketed lists, except that the field name is separated from the field's type with a colon ``:`` instead of an equal sign ``=``. So the type of the above record is ``<a : Str, b : Bool>``.

We can access the fields of a record by using the projection operator ``|``.

Example e-1.6::

    let r : <a : Str, b : Bool> =
      <a = "bloob", b = false>;

    ( r|a );

Unlike many other languages, the parentheses around the infix projection operation are mandatory.::

    > ( r|a );
    "bloob"
    : Str

    > ( r|b );
    false
    : Bool

    
Functions
^^^^^^^^^

This section is about functions. In Cuneiform, functions can be either native, which means that their evaluation is performed by the Cuneiform interpreter, or foreign, which means that their evaluation is performed by a worker. Foreign functions can be written in any one of the supported scripting languages, e.g., R or Python.

Functions take a number of arguments and produce a return value. A function definition provides the function name, the names and types of all arguments, and the type of the return value. In the case of a foreign function, we also need to provide the name of the foreign language.

The following example defines a function ``add`` with two arguments ``a`` and ``b`` which are both strings. The return value's type is a record with a single field ``c`` of type string. The foreign language is Perl.

.. _e-1-6:

Example e-1.6::
	
    def add( a : Str, b : Str ) -> <c : Str> in Perl *{
      $c = $a+$b;
    }*
    
A function definition starts with the keyword ``def`` followed by the function name, which is here ``add``. Next is the function signature declaring two arguments ``a`` and ``b`` of type ``Str``. The return type is ``<c : Str>``.

The Perl part adds the values of ``a`` and ``b`` and stores the result in the variable ``c``.

Foreign functions must always return a record. Each field of this record is associated with the value of a variable bound to the same name in the foreign language. 

We can now apply this function like so

Example e-1.7::
	
    add( a = "1", b = "2" );
    
This function application binds the argument ``a`` to the string literal ``"1"`` and argument ``b`` to the string literal ``"2"``::

    > add( a = 1, b = 2 );
    <c = "3">
    : <c : Str>
    
Let's look at another example for a function definition. This time, we want to concatenate two strings. We choose to perform this operation in R.

Example e-1.8::
	
    def concat( a : Str, b : Str ) -> <c : Str> in R *{
      c = paste( a, b )
    }*

    concat( a = "Hello ", b = "world." );
    
Applying ``concat`` to the string literals ``"Hello "`` and ``"world."`` results in a record with a single field ``<c = "Hello world">``.


Assignments
-----------

Assignment a-1.1
^^^^^^^^^^^^^^^^

Define a Cuneiform function in Perl that takes one argument and computes the square
of that argument.

Assignment a-1.2
^^^^^^^^^^^^^^^^

How would a ``concat`` foreign function definition look in Python or Bash?

Assignment a-1.3
^^^^^^^^^^^^^^^^
   
Assuming you have defined ``let x : Str = "5";`` defining ``let y : Str = x;`` makes the variable ``y`` have the same value as ``x`` being ``"5"``. What happens to the binding of ``y`` if you update the value of ``x`` to, say, ``"6"``? Explain your reasoning. Use Cuneiform's interactive shell and its features.
    
   
Solutions
---------

Solution a-1.1
^^^^^^^^^^^^^^^^

::

    def square( a : Str ) -> <b : Str> in Perl *{
      $b = $a*$a;
    }*
    
    square( a = 5 );
    
Solution a-1.2
^^^^^^^^^^^^^^^^

::

    def concat2( a : Str, b : Str ) -> <c : Str> in Python *{
      c = a+b
    }*
    
    def concat3( a : Str, b : Str ) -> <c : Str> in Bash *{
      c="$a$b"
    }*
    
    concat2( a = "bla", b = "blub" );
    concat3( a = "sha", b = "lala" );
        
    
Solution a-1.3
^^^^^^^^^^^^^^^^

Given the following definitions::

    let x : Str = 5;
    let y : Str = x;
    
On updating the variable ``let x : Str = 6;`` the variable ``y`` keeps its value because it refers to a different definition of ``x`` than the current one. This is called shadowing. It is impossible to taint old definitions by rebinding variables. The current ``x`` is a different variable than the ``x`` appearing in the definition of ``y``. Using the ``hist`` command shows all definitions in the order they were introduced. Shadowed definitions are also shown.



