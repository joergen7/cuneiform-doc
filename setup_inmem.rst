In-memory Setup
===============

This section describes how to set up Cuneiform in-memory which can give it an
immense speed up if intermediate and ouput data are small. The guide assumes
that a :ref:`setup_chef_local` is in place.

Setting Up a RAM File System
----------------------------

First, we need to set up a RAM file system. The corresponding reproduce a
`Howto by James Coyle <http://www.jamescoyle.net/how-to/943-create-a-ram-disk-in-linux>`_.

To create a RAM file system limited to 8GB in the mount point /mnt/ramdisk
permanently, create a corresponding entry in the /etc/fstab::
	
    tmpfs	/mnt/ramdisk	tmpfs	nodev,nosuid,nodiratime,size=8192M	0 0

You need to restart your system for the change to take effect.
    
Setting Cuneiform's Cache Directory
-----------------------------------

The Cuneiform command line interface offers the -l parameter to set the local
cache. By setting it to /mnt/ramdisk/cf-cache we can make Cuneiform store all
intermediate and output data in the RAM file system.

If you used the `Cuneiform Chef cookbook <https://github.com/joergen7/chef-cuneiform>`_, the Cuneiform executable should be in
/usr/local/bin/cuneiform. Now open it and change the value of the -l option from
/tmp/cf-cache to /mnt/ramdisk/cf-cache. Afterwards, the Java command should look like
this::

    #!/usr/bin/env bash
    nice -n 19 java -cp "..." de.huberlin.wbi.cuneiform.cmdline.main.Main -l /mnt/ramdisk/cf-cache $@
    
Cuneiform will now run in-memory, never exceeding its 8GB bound.
