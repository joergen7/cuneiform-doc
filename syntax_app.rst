.. _syntax_app:

Application (app)
=================

An Application (app) can be either explicit or an implicit. An explicit
Application starts with the keyword ``apply`` and binds the special parameter
``task`` to a :ref:`syntax_compoundexpr` of Task Definitions. An implicit
application is equivalent to an explicit application with exactly one task ID.

A :ref:`syntax_expr` can be an Application.

**app:**

.. image:: img/app.png

::

    app ::= 'apply' '(' 'task' ':' compoundexpr ( ',' binding )* ')'
          | ID '(' ( binding ( ',' binding )* )? ')'
    
References:

- :ref:`syntax_compoundexpr`
- :ref:`syntax_binding`

ID:
   An ID is a regular string beginning with a letter and containing letters,
   numbers, or the symbols -, _, +, \*, or / and not being a keyword.

Examples
--------

An implicit Application of the task ``sim`` consuming no input parameters::
	
    sim()
    
An implicit Application of the task ``greet`` binding its only parameter ``person``
to a Compound Expression consisting of three string literals::
	
    greet( person: "Jenny" "Peter" "John" )
    
An explicit Application of the task sim::
	
    apply( task: sim )
    
An explicit application of the tasks ``bowtie2-align`` and ``bwa-align`` binding
their two input parameters ``idx`` and ``fastq``::
	
    apply( task:  bowtie2-align bwa-align,
           idx:   bowtie2-idx bwa-idx
           fastq: fastq )
