Quick Start
===========

This section gives a brief introduction to working with Cuneiform. It shows, how
to set up Cuneiform in a Virtual Machine (VM), and run a Hello World workflow.

.. note::
   Since Cuneiform will run in a Virtual Machine, this setup has no special
   requirements towards your operating system or Java version. Root access is
   required only for installing the prerequisites.

Prerequisites
-------------

The following software has to be available on your system:

- `Git <https://git-scm.com/>`_
- `VirtualBox <https://www.virtualbox.org/>`_
- `Chef Development Kit <https://downloads.chef.io/chef-dk/>`_
- `Vagrant <https://www.vagrantup.com/>`_

.. attention::
   When installing Git on Windows, make sure to select
   *Use Git from the Windows Command Prompt* when asked to adjust your PATH
   environment.
   
.. hint::
   If you are running a Debian-based operatin system you can install these
   packages simply by entering::

       sudo apt-get install -y gdebi
       wget https://opscode-omnibus-packages.s3.amazonaws.com/debian/6/x86_64/chefdk_0.10.0-1_amd64.deb
       sudo gdebi chefdk_0.10.0-1_amd64.deb
       sudo apt-get install git virtualbox vagrant

Setting up a VM
---------------

Clone the `chef-cuneiform <https://github.com/joergen7/chef-cuneiform>`_
repository by opening a command line terminal and entering::
	
    git clone https://github.com/joergen7/chef-cuneiform.git

.. hint::
    If you are living behind a proxy then update the ``.kitchen.yml`` file in the ``chef-cuneiform`` folder by updating the ``provisioner:`` entry as follows:

    .. code-block:: yaml

        provisioner:
          name: chef_zero
          http_proxy: http://proxy.example.com:PORT
          https_proxy: http://proxy.example.com:PORT
    
Change into the cloned directory and have Chef create a VM by entering::
	
    cd chef-cuneiform
    kitchen converge
    
The process of setting up the VM may take a few minutes depending on your
internet connection. A Ubuntu 14.04 image is fetched from the internet and a
Java environment is set up in the VM. All dependencies are installed and
the Cuneiform source code is downloaded and compiled.

.. hint::
   To destroy the VM again after using it, enter::

       kitchen destroy
       
Preparing a Workflow
--------------------

You can login to the VM by entering

    kitchen login
    
You can create a workflow file using an editor. Here, we are using nano to
create a workflow file *hello.cf*::
	
    nano hello.cf
    
Now enter (or copy/paste) the following Cuneiform source code in the editor
window::
	
    deftask greet( out : person )in bash *{
      out="Hello $person"
    }*
    
    greet( person: "Peter" "Robert" );
    
Save and close the workflow file by pressing Ctl+X.

.. note::
   We could have entered the Task Definition and the Application in any order.

The workflow you just created defines a single task *greet* with one output
parameter *out* and one input parameter *person*. Whatever string is bound to
the parameter *person* is prepended a Hello and returned via the output
parameter *out*.

In the next step we apply the just created task *greet* to a list with two
string literals *"Peter"* and *"Robert"*.

Running the Workflow
--------------------

To run the workflow we just created inside the VM, we enter in the command line
terminal::
	
    cuneiform hello.cf
    
The output should look something like this::
	
    INFO  Query 633aeb81-3885-4203-b813-acd6e33a01b2 started.
    INFO  Query 633aeb81-3885-4203-b813-acd6e33a01b2 finished: 'Hello Peter' 'Hello Klaus'

    
    
    
