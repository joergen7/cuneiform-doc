Integration and Build
=====================

Adding Effi to a Project
------------------------

Although Effi can be imported also directly from GitHub, we recommend adding a dependency via `hex.pm <https://hex.pm>`_. Here, we show how this can be done using the build tools `rebar3 <https://www.rebar3.org>`_ or mix.


rebar3
^^^^^^

To integrate effi into a rebar3-managed project change the ``deps`` entry in your application's ``rebar.config`` file to include the tuple ``{effi, "0.1.6"}``

.. code-block:: erlang

    {deps, [{effi, "0.1.6"}]}.

mix
^^^

To integrate effi into a mix-managed project include the following

.. code-block:: elixir

    {:effi, "~> 0.1.6"}

Compiling
---------

Having rebar3 available on your system, compile as an Erlang project by entering::

    rebar3 compile

If you want to drive the project from the command line please compile it by entering::

    rebar3 escriptize

