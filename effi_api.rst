Erlang API
==========

Effi can be driven from an Erlang API by using the function ``effi:handle_request/2``. Given an Erlang hash map using atoms as keys and binaries as values bound in the variable ``EffiRequest`` you can start effi by entering::

    EffiRequest = #{ ... }.
    Dir = "./".
    effi:handle_request( EffiRequest, Dir ).

Effi starts evaluating the request, expecting input data in and writing output data to the working directory given in the variable ``Dir``.

The ``handle_request/2`` function returns a reply-map summarizing the result of the computation.
