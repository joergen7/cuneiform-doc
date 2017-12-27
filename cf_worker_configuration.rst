.. _cf_worker_configuration:

Configuration
=============

Default Configuration
---------------------

If no other configuration is provided, the Cuneiform worker application uses the following default configuration:

.. code-block:: json

   {
     "n_wrk":    "auto",
     "cre_node": "node"
   }

This configuration can be superseded by

- creating a *global* configuration file with a subset of the above entries in :code:`/usr/local/etc/cuneiform/cf_worker.json`
- creating a *user-specific* configuration file with a subset of the above entries in :code:`~/.config/cuneiform/cf_worker.json`
- providing a custom configuration file from the command line (see :ref:`cf_worker_deployment`)
- providing explicit command line flags (see :ref:`cf_worker_deployment`)

Configuration Entries
---------------------

The Cuneiform worker application has the following configuration entries:

- :code:`n_wrk` The number of worker processes to start under this application master. A positive integer or the string :code:`"auto"`. If the entry is set to :code:`"auto"`, the application tries to guess the number of cores on the machine and start as many workers. If the number of cores could not be determined, one worker process is started.
- :code:`cre_node` The Erlang node name on which the CRE application is running. Any string or :code:`"node"`. If the entry is set to :code:`"node"` the CRE application is looked up on the current Erlang node.

.. attention::
   Leaving the CRE node at the default value :code:`"node"` will most likely result in an error. Typically, if the CRE computer's hostname is :code:`my_host` you need to set the CRE Erlang node to :code:`"cre@my_host"`. However, you have the freedom to set this parameter as early as in the global configuration file or as late as on the command line.