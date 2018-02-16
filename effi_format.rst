Exchange Formats
================

Effi is driven by task instantiations or applications. Running effi on an application results in a reply. Here, we describe the application format and the reply format.

Example
-------

.. code-block:: json

  { "app_id": "1234",
    "lambda": { "lambda_name":  "bowtie2-build",
                "arg_type_lst": [{ "arg_name": "fa",
                                   "arg_type": "File",
                                   "is_list":  false }],
                "ret_type_lst": [{ "arg_name": "idx",
                                   "arg_type": "File",
                                   "is_list":  false }],
                "lang":         "Bash",
                "script":       "bowtie2-build $fa bt2idx\nidx=idx.tar\ntar cf $idx --remove-files bt2idx.*\n" },
    "arg_bind_lst": [{ "arg_name": "fa",
                       "value":    "chr22.fa" }] }

.. code-block:: json

  { "app_id":          "1234",
    "stat":            { "tstart":   "...",
                         "duration": "..." },
    "result":          { "status":   "ok",
                         "ret_bind_lst": [{ "arg_name": "idx",
                                            "value":    "idx.tar" }] } }

Application Format
------------------

The application format is what effi consumes. An application :code:`App` has the following form:

.. code-block:: none

  App ::= { "app_id":       S,
            "lambda":       Lambda, 
            "arg_bind_lst": [Bind, ...] }

The application's lambda expression :code:`Lambda` has the following form:

.. code-block:: none

  Lambda ::= { "lambda_name":  S,
               "arg_type_lst": [TArg, ...],
               "ret_type_lst": [TArg, ...],
               "lang":         Lang,
               "script":       S }

A lambda expression's :code:`arg_type_lst` pair lists specifications for the input parameters while the :code:`ret_type_lst` pair lists specifications for the output parameters of a lambda. An input or output parameter specification :code:`TArg` has the following form:

.. code-block:: none

  TArg ::= { "arg_name": S,
             "arg_type": Type,
             "is_list":  B }

The :code:`arg_type` pair provides the base type of the argument. The base type :code:`Type` has the following form:

.. code-block:: none

  Type ::= "Bool"
         | "Str"
         | "File"


The :code:`lang` pair provides the programming language in which the script is written. The language :code:`Lang` has the following form:

.. code-block:: none

  Lang ::= "Bash"
         | "Octave"
         | "Perl"
         | "Python"
         | "R"
         | "Racket"

A lambda expression contains a list of argument bindings :code:`Bind` of the following form:

.. code-block:: none

  Bind ::= { "arg_name": S, "value": S}
         | { "arg_name": S, "value": [S, ...] }

.. code-block:: none

  B ::= true
      | false

.. code-block:: none

  S ::= "..."

Reply Format
------------

The reply format is what effi produces.

.. code-block:: none

  Reply ::= { "app_id": S,
              "stat":   { "t_start": S, "duration": S },
              "result": Result }


.. code-block:: none

  Result ::= { "status": "ok", "ret_bind_lst": [Bind, ...] }
           | { "status": "error", "stage": "run", "extended_script": S, "output": S }
           | { "status": "error", "stage": "stagein", file_lst: [S, ...] }
           | { "status": "error", "stage": "stageout", file_lst: [S, ...] }

