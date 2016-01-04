.. _setup_compile:

Compiling from Source
=====================

Instead of downloading the binaries from the
`Cuneiform Download page <http://cuneiform-lang.org/download/>`_, you can
download the `Cuneiform source code <https://github.com/joergen7/cuneiform>`_
and compile the binaries yourself.

.. note::
   This guide is written assuming you are running a Ubuntu operating system.
   The instructions may work identically on other Debian-based Linux
   distributions and should apply with only minor modifications to
   Unix-based operating systems like Suse, CentOS, Fedora, or Mac OS.
   
.. note::
   Compiling the source code requires no root access.
   
Prerequisites
-------------

To compile Cuneiform from its source you need to install the following packages:

- git
- openjdk-7-jdk
- maven

To do so, enter in a command line terminal::
	
    sudo apt-get install git openjdk-7-jdk maven

Download and Compile
--------------------

First, clone the Cuneiform source code repository from GitHub::
	
    git clone https://github.com/joergen7/cuneiform.git
    
After entering the repository's directory compile the source code using maven::
	
    cd cuneiform
    mvn clean package
    
The compiled binaries are now located in the directory ./cuneiform-dist/target.
