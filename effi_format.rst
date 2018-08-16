Effi JSON Exchange Format
=========================

Effi is driven by task instantiations or applications. Running effi on an application results in a reply. Here, we describe the application format and the reply format.

Example
-------

Below is an example for an Effi request (an application)

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

The following is an example for an Effi reply:


.. code-block:: json

    { "app_id": "1234",
      "result": { "status":       "ok",
                  "stat":         { "run":  { "t_start":  "1523007609917834743",
                                              "duration": "30391761645" },
                                    "node": "cf_worker@x240" },
                  "ret_bind_lst": [{ "arg_name": "idx",
                                     "value":    "idx.tar" }] } }

The start time `tstart` is given in nanoseconds from 1970-01-01 and also the the wall-clock running time `duration` is given in nanoseconds. So the example ran `bowtie2-build` for about 30.4 seconds. The `node` field identifies the Erlang node name of the worker instance that ran the task.

Request Format
--------------

The Effi request (application) format is what is consumed. An application `App` has the following form:

.. code-block:: none

    App ::= { "app_id":       S,
              "lambda":       Lambda, 
              "arg_bind_lst": [Bind, ...] }

The application's lambda expression `Lambda` has the following form:

.. code-block:: none

    Lambda ::= { "lambda_name":  S,
                 "arg_type_lst": [TArg, ...],
                 "ret_type_lst": [TArg, ...],
                 "lang":         Lang,
                 "script":       S }

A lambda expression's `arg_type_lst` pair lists specifications for the input parameters while the `ret_type_lst` pair lists specifications for the output parameters of a lambda. An input or output parameter specification `TArg` has the following form:

.. code-block:: none

    TArg ::= { "arg_name": S,
               "arg_type": Type,
               "is_list":  B }

The `arg_type` pair provides the base type of the argument. The base type `Type` has the following form:

.. code-block:: none

    Type ::= "Bool"
           | "Str"
           | "File"


The `lang` pair provides the programming language in which the script is written. The language `Lang` has the following form:

.. code-block:: none

    Lang ::= "Bash"
           | "Matlab"
           | "Octave"
           | "Python"

A lambda expression contains a list of argument bindings `Bind` of the following form:

.. code-block:: none

    Bind ::= { "arg_name": S, "value": S}
           | { "arg_name": S, "value": [S, ...] }

    B ::= true
        | false

    S ::= "..."

Reply Format
------------

The Effi reply format is what is produced.

.. code-block:: none

    Reply ::= { "app_id": S,
                "result": Result }

    Result ::= { "status": "ok",
                 "stat":   { "run":  { "t_start": S, "duration": S },
                             "node": S },
                 "ret_bind_lst": [Bind, ...] }
             | { "status": "error", "stage": "run", "extended_script": S, "output": S }
             | { "status": "error", "stage": "stagein", file_lst: [S, ...] }
             | { "status": "error", "stage": "stageout", file_lst: [S, ...] }



