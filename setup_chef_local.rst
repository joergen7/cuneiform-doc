.. _setup_chef_local:

Local Setup with Chef
=====================

This section describes how to set up Cuneiform locally on your machine. In
addition to fetching and compiling the Cuneiform
`source code <https://github.com/joergen7/cuneiform>`_ it creates executables in
suitable locations, installing Cuneiform for all users.

.. note::
   This guide assumes you are running an Ubuntu Linux 14.04. While later
   versions of Ubuntu should work as well, it is not recommended to run this
   cookbook on operating systems other than Ubuntu.

.. note::
   Since Chef installs packages and creates executables in system directories,
   it requires root access.
   
If you are not running Ubuntu or do not have root access to your machine,
please refer to the :ref:`setup_chef_vm`. If creating a VM is also no option
for you, consider downloading the
`Cuneiform binaries <http://www.cuneiform-lang.org/download/>`_
or :ref:`setup_compile`.
   
Prerequisites
-------------

Please install the following packages:

- git
- chefdk


.. hint::
   You can do so by entering in a command line terminal::
	
       sudo apt-get install git chefdk
    
    
Download and Install
--------------------

First, create a directory *cookbooks* and enter it::
	
    mkdir cookbooks
    cd cookbooks

Clone into the cookbooks directory the
`Cuneiform Chef cookbook <https://github.com/joergen7/chef-cuneiform>`_ by
entering::
	
    git clone https://github.com/joergen7/chef-cuneiform.git
    
Now enter the directory just above the *cookbooks* directory and run the Chef
client::
	
    cd ..
    sudo chef-client -z -r "chef-cuneiform::default"

.. attention::
   All applications that may hold a lock on the package management system, like
   Synaptic, dpkg, or apt-get, must be closed.
   
Check the success of the installation by observing the output of::
	
    cuneiform --help
