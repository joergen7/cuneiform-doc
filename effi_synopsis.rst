Command Line Synopsis
=====================

Compiling effi using ``escriptize`` creates an Erlang script file ``effi`` whcih allows starting it via the command line.

To display a help text enter::

    ./effi --help

This shows the command line synopsis, which looks like the following::

       ._,,,,  ,,_,=_
        W   `_@__#__     The Erlang Foreign Function Interface (Effi) allows the
       @P+#   F @F @     execution of functions defined in different programming
      _W   y @  # qF     languages (e.g., Bash, Python, or R) by specifying the
      ^^^^^  P qF  `     function's arguments, body and output values.

    Copyright 2015-2018 Jorgen Brandt <joergen.brandt@onlinehome.de>

    Usage: effi [-v] [-h] [-d [<dir>]] [-i <input_file>] [-o <output_file>]

      -v, --version      Show effi version.
      -h, --help         Show command line options.
      -d, --dir          Working directory in which to look for input data and 
                         run the request. [default: .]
      -i, --input_file   Input file holding the effi request (must be 
                         specified).
      -o, --output_file  Output file into which to write the effi reply (must 
                         be specified).


    The input_file and output_file arguments must be specified.

To start Effi from the command line consuming the request file ``effi_request.json`` and let it produce the reply file ``effi_reply.json`` enter::

    ./effi -i effi_request.json -o effi_reply.json

The format of the request and reply is described below.

