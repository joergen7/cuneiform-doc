.. _setup_compile:

Compiling from Source
=====================

Instead of downloading the binaries from the
`Cuneiform Download page <http://cuneiform-lang.org/download/>`_, you can
download the `Cuneiform source code <https://github.com/joergen7/cuneiform>`_
and compile the binaries yourself.

.. note::
   This guide is written assuming you are running a Ubuntu 15.10 or higher.
   The instructions may work identically on other Debian-based Linux
   distributions and should apply with only minor modifications to
   Unix-based operating systems like Suse, CentOS, Fedora, or Mac OS.
   
.. note::
   Compiling the source code requires no root access.
   
Prerequisites
-------------

To compile Cuneiform from its source you need to install the following packages:

- git
- erlang

To do so, enter in a command line terminal::
	
    sudo apt-get install git erlang

Make sure that you are running an Erlang emulater version 7.0 (OTP 18.0) or higher. You can check your Erlang version by entering::

    erl -version

Additionally an installation of Rebar 3.0 is necessary. Download and compile Rebar 3.0 by entering::

    git clone https://github.com/erlang/rebar3.git
    cd rebar3
    ./bootstrap

To install Rebar 3.0 on your system enter::

    sudo cp rebar3 /usr/local/bin

Download and Compile
--------------------

First, clone the Cuneiform source code repository from GitHub::
	
    git clone https://github.com/joergen7/cuneiform.git
    
After entering the repository's directory compile the source code using Rebar 3.0::
	
    cd cuneiform
    make
    
The compiled binaries are now located in the directory `_build/default/bin`. To install Cuneiform permanently on the system enter::

    make install