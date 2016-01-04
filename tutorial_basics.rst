Cuneiform Basics
================

Learning Objective
  This tutorial introduces you to fundamental Cuneiform language concepts.
  You will use the Cuneiform interactive shell, to define tasks, 
  assign variables and query your workflow. These concepts are illustrated with
  simple examples showing string manipulation and arithmetic operations.
  Furthermore, you  will familiarize yourself with Cuneiform's Call-By-Name
  evaluation strategy.
      
Difficulty
  Basic
  
Duration
  45 min
  
Prerequisites
  Basic programming background. A working installation of Cuneiform (see
  :ref:`setup` section).
  

Introduction
------------

This tutorial is an introduction to the most important concepts of Cuneiform
which you will need to use in all but the most simplistic scenarios. This is
assigning expressions to variables, querying, and defining tasks. In later
tutorials when more specialized language concepts are introduced it is important
for you to be familiar with the basic concepts covered in this tutorial. These
basic concepts lets you specify arbitrarily complex workflows driving APIs from
Perl, R, Python, and Bash. After this tutorial will be able to define tasks,
apply tasks, assign variables and query the value of an expression.
      
Explanation and Examples
------------------------
  
Statements
^^^^^^^^^^

Statements are the building blocks of a Cuneiform
:ref:`syntax_script`. There are 3 kinds of Statements: (i) Assignments, (ii)
Queries, and (iii) Task Definitions. This section is supposed to give you a
quick overview about the 3 :ref:`syntax_stat` types:

:ref:`syntax_assign`
    Assignments bind expressions to variables.

:ref:`syntax_query`
    Queries tell the interpreter which values you are interested in. Only
    computation steps actually contributing to these values are executed.

:ref:`syntax_defun`
    Task Definitions are much like function definitions.

Unless specifying very simplistic workflows, we have to use of each kind of
Statement.

Assignments
^^^^^^^^^^^

Assignments are used to assign an expression to a
variable. Variables can be used to hold workflow outputs which can later be
queried (see `Queries`_) or to hold intermediate results to be reused in other
parts of a workflow. This section is supposed to show you how to use assignments
along with introducing a basic kind of expression: the literal.

To reproduce the examples below, start the Cuneiform interactive shell by
entering on the command line::

    cuneiform -i
  
.. hint::
   You can exit the Cuneiform interactive shell by entering ``quit;``.
  
An Assignment binds an expression to a variable. Where the variable name appears
on the left-hand side of an equals symbol while the expression to be bound
appears on the right-hand side.

Example e-1.1::
	
    x = 5;
    
In this example we have bound the integer literal ``5`` to the variable ``x``.
Let's look at another example.

Example e-1.2::

    person = "Peter";
    
Here, the expression is the string literal ``"Peter"`` while the variable is
``person``. An assignment declares to the Cuneiform interpreter that whenever it
sees a variable like ``x`` or ``person`` the interpreter should shellace that
variable with whatever expression is bound to it. You will see later, that it is
possible to assign quite complex expressions. Nevertheless, an assignment never
triggers any computation. It just binds an (unevaluated) expression to a
variable.

Queries
^^^^^^^

This section is about querying a Cuneiform workflow. While Assignments and 
Task Definitions constitute the dependency graph of a workflow, they are in
themselves just declarations describing a workflow. A query, on the other hand,
defines the goal of a workflow. This section is supposed to show how a workflow
is queried.

In a query you tell the Cuneiform interpreter what value you are interested in.
Queries are the only kind of Statement, that actually trigger a computation. A
Query can be any kind of expression terminated with a semicolon. To find out the
value of the variable ``person`` we can query it.

Example e-1.3::
	
    person;
    
Assuming you have also entered Example e-1.2, you should get an output like this
on the Cuneiform interactive shell::
	
    > person;
    INFO  Query 3394b425-7b94-472d-a3c6-0509f3fffda5 started.
    INFO  Query 3394b425-7b94-472d-a3c6-0509f3fffda5 finished: 'Peter'

Some queries are special in the sense, that they do not trigger a computation
but a side effect. We have already encountered one such special query: ``quit;``
which exits the shell. Another important special query is ``state;`` which
prints out all variable bindings which the shell has collected so far. Assuming
you entered Examples e-1.1 and e-1.2, you should get something like this on
entering ``state;``

Example e-1.4::
	
    > state;
    x = '5';
    person = 'Peter';
    
Task Definition and Application
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This section is about tasks which take a prominent role in Cuneiform and are the
equivalent to functions in general purpose programming languages. In Cuneiform,
tasks can be in any foreign scripting language. This section is supposed to show
how to define tasks and apply them.

Cuneiform lets you define tasks. We call them tasks to emphasize their origin in
scientific workflows but actually they are much like functions. They take a
number of arguments and return an output value. You define and apply tasks in
much the same way you would define and apply functions in any general purpose
programming language.

One strong point of Cuneiform is, that it is simple to define tasks in languages
other than Cuneiform itself. This allows Cuneiform to be very simple (and, thus,
easy to learn) while, at the same time, to tap the potential of all the
supported foreign languages.

Let's look at an example adding two numbers

Example e-1.5::
	
    deftask add( c : a b )in perl *{
      $c = $a+$b;
    }*
    
A Task Definition starts with the keyword ``deftask`` followed by the task name,
which is here ``add``. Next is the :ref:`syntax_sign` declaring one output
variable ``c`` and, separated by a ``:``, two input variables ``a`` and ``b``.
Furthermore, we state that the task body will be written ``in perl``.

The Perl part adds the values of ``a`` and ``b`` and stores the result in the
variable ``c``. We can now apply this task like so

Example e-1.6::
	
    add( a: 1, b: 2 );
    
In this :ref:`syntax_app` we have bound the input variable ``a`` to the integer
literal ``1`` and the input variable ``b`` to the integer literal ``2``.
Assuming you have entered Examples e-1.5 and e-1.6 you should get an output like
this::
	
    > add( a: 1, b: 2 );
    INFO  Query e2d93732-1488-4be3-83af-f5e959c9681b started.
    INFO  Query e2d93732-1488-4be3-83af-f5e959c9681b finished: '3'
    
Let's look at another example for a Task Definition. This time, we want to
concatenate two strings. We choose to perform this operation in R.

Example e-1.7::
	
    deftask concat( c : a b )in r *{
      c = paste( a, b )
    }*

    concat( a: "Hello ", b: "world." );
    
Applying ``concat`` to the string literals ``"Hello "`` and ``"world."``
evaluates to the string literal ``"Hello world."``.


Assignments
-----------

Assignment a-1.1
^^^^^^^^^^^^^^^^

Define a Cuneiform task in Perl that takes one argument and computes the square
of that argument.

Assignment a-1.2
^^^^^^^^^^^^^^^^

How would a ``concat`` task look in Python or Bash?
    
.. hint::
   You do not need to be an expert in Python or Bash to complete this task.
   Googling "concatenate two strings in python" should give you something you
   can pretty much copy and paste.

Assignment a-1.3
^^^^^^^^^^^^^^^^
   
Assuming you have assigned ``x = 5;`` assigning ``y = x;`` makes the
variable ``y`` have the same value as ``x`` being ``5``. Will anything
happen to the value of ``y`` if you update the value of ``x`` to, say,
``6``? Explain your reasoning. Try it out in the Cuneiform interactive shell.
    
   

