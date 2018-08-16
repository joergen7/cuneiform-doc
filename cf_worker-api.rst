Erlang API
==========

If a CRE instance is already running on the same Erlang node you can start the Cuneiform worker application by calling

.. code-block:: erlang

    cf_worker:start().


Which is exactly the same as calling


.. code-block:: erlang

    application:start( cf_worker ).


Starting Under the Default Supervisor
-------------------------------------

To start the Cuneiform worker default supervisor under a custom supervision tree enter

.. code-block:: erlang

    CreNode = node().
    NWrk    = 4.
    WrkDir  = "./_cuneiform/wrk".
    RepoDir = "./_cuneiform/repo".
    DataDir = "./".

    cf_client_sup:start_link( CreNode, NWrk, WrkDir, RepoDir, DataDir ).


This starts a worker supervisor with four workers using ``WrkDir`` to store temporal data, ``RepoDir`` for intermediate and output data, and `DataDir` to look up input data. Also, we expect a CRE to be running on the same node.

Starting Directly
-----------------

The Cuneiform client process can be started directly. There are several ways to do this. The first is to start the process with a function that allows it to locate the CRE:

.. code-block:: erlang

    CreNode = node().
    F = fun() -> cre:pid( CreNode ) end.

    WrkDir  = "./_cuneiform/wrk".
    RepoDir = "./_cuneiform/repo".
    DataDir = "./".

    {ok, WorkerPid} = cf_worker_process:start_link( F, WrkDir, RepoDir, DataDir ).

Giving a function instead of a plain CRE process identifier has the advantage, that if the CRE crashes, taking the Cuneiform worker with it, the restarted worker instance uses the output of the function, which offers the possibility of locating the CRE under its new process identifier.

If this is too tedious, one can start it giving the CRE process identifier directly:

.. code-block:: erlang

    CrePid = cre:pid( node() ).

    WrkDir  = "./_cuneiform/wrk".
    RepoDir = "./_cuneiform/repo".
    DataDir = "./".

    {ok, WorkerPid} = cf_worker_process:start_link( CrePid ).


Both previous direct starting methods do not register the Cuneiform client with any registry service.

