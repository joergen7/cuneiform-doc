.. _cf_worker_deployment:

Usage
=====

The Cuneiform worker application (cf_worker) needs to connect to a :ref:`cre`. Thus, in order to start a Cuneiform worker, the Erlang node name of the CRE instance needs to be known (e.g., :code:`cre@x240`).

Command Line
------------

.. code-block:: none

  Usage: cf_worker [-v] [-h] [-c <suppl_file>] [-r <cre_node>]
                   [-n [<n_wrk>]]

    -v, --version     Show cf_worker version.
    -h, --help        Show command line options.
    -c, --suppl_file  Supplementary configuration file.
    -r, --cre_node    Erlang node running the CRE application (must be 
                      specified).
    -n, --n_wrk       Number of worker processes to start. 0 means 
                      auto-detect available processors. [default: 0]

  The cre_node argument must be specified.


Driving the Application from Erlang
-----------------------------------

