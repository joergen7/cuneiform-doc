System Requirements
===================

There are no special hardware requirements. Nevertheless, your system should be able to host all workflow
applications and have a hard drive that is able to store all input, intermediate and output data of a
workflow run.

If you intend to run Cuneiform in-memory, your main memory must be capable to hold all intermediate data.

Supported Operating Systems:

- Linux
- Mac OS

.. warning::
    Windows is currently not supported by Cuneiform. The reason is that Cuneiform
    relies on a Posix-like environment.
 
Additionally, Cuneiform requires Erlang emulator version 7.0 (OTP 18.0)  or higher. You can check your Erlang version by entering::
	
    erl -version
