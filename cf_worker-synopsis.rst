Command Line Synopsis
=====================

Compiling the Cuneiform client using ``escriptize`` creates an Erlang script file ``cf_worker`` which allows starting the Cuneiform client via the command line.

To display a help text enter

.. code-block:: none

    ./cf_worker --help

This will show the command line synopsis, which looks like the following:

.. code-block:: none

    Usage: cf_worker [-v] [-h] [-s <suppl_file>] [-c <cre_node>] [-n <n_wrk>]
                     [-w <wrk_dir>] [-r <repo_dir>] [-d <data_dir>]

      -v, --version     Show cf_worker version.
      -h, --help        Show command line options.
      -s, --suppl_file  Supplementary configuration file.
      -c, --cre_node    Erlang node running the CRE application (must be 
                        specified).
      -n, --n_wrk       Number of worker processes to start. 0 means 
                        auto-detect available processors.
      -w, --wrk_dir     Working directory in which workers store temporary 
                        files.
      -r, --repo_dir    Repository directory for intermediate and output data.
      -d, --data_dir    Data directory where input data is located.


To start the worker application from the command line and connect with a running CRE instance enter

.. code-block:: none

    ./cf_worker -c cre@my_node

Here, we assume that the CRE runs on an Erlang node identified as ``cre@my_node``.

