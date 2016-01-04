.. _syntax_query:

Query (query)
=============

A Query (query) is a :ref:`syntax_compoundexpr` terminated with a semicolon.

A :ref:`syntax_stat` can be a Query.

**query:**

.. image:: img/query.png

::

    query        ::= compoundexpr ';'
    
References:

- :ref:`syntax_compoundexpr`

Examples
--------

Querying the ID *result*::
	
    result;
    
The application of the task *sim* as a query::
	
    sim();
