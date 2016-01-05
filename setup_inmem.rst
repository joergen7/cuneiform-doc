In-memory Setup
===============

This section describes how to set up Cuneiform in-memory which can give it an
immense speed up if intermediate and ouput data are small. The guide assumes
that a :ref:`setup_chef_local` is in place.

Setting Up a Temporary File System
----------------------------

A prerequisite for running Cuneiform in-memory is the existence of a temporary
file system. Most Linux distributions come with such a RAM file system already
set up by default. The mount point of this default temporary disk is
``/dev/shm``. You can verify its existence by entering in a command line
terminal::
	
    df -h
    
Here, the parameter ``-h`` lets ``df`` output the file system sizes in
human-readable format. The output may look something like this::
	
    Filesystem      Size  Used Avail Use% Mounted on
    udev            7,8G     0  7,8G   0% /dev
    tmpfs           1,6G   18M  1,6G   2% /run
    /dev/sdb2       901G  167G  688G  20% /
    tmpfs           7,9G  324K  7,9G   1% /dev/shm
    tmpfs           5,0M  4,0K  5,0M   1% /run/lock
    tmpfs           7,9G     0  7,9G   0% /sys/fs/cgroup
    /dev/sdb1       511M  3,4M  508M   1% /boot/efi
    tmpfs           1,6G   44K  1,6G   1% /run/user/1000
    
The last column with the column header ``Mounted on`` tells us the mount point
of each listed file system. From this example, we can see that a temporary file
system of 8GB size is mounted under ``/dev/shm``. We can just use it.

If no temporary file system is preconfigured, we need to do so, ourselves. To
create a temporary file system limited to 8GB in the mount point
``/mnt/ramdisk`` permanently, create a corresponding entry in the /etc/fstab::
	
    tmpfs	/mnt/ramdisk	tmpfs	nodev,nosuid,nodiratime,size=8192M	0 0

You need to restart your system for the change to take effect or enter on the
command line::
	
    sudo mount /mnt/ramdisk
    
Setting Cuneiform's Cache Directory
-----------------------------------

The Cuneiform command line interface offers the ``-l`` parameter to set the
local cache. By setting it to ``/dev/shm/cf-cache`` we can make Cuneiform store
all intermediate and output data in the temporary file system.

If you used the `Cuneiform Chef cookbook <https://github.com/joergen7/chef-cuneiform>`_,
the Cuneiform executable should be in ``/usr/local/bin/cuneiform``. Now open it
and change the value of the ``-l`` option from ``/tmp/cf-cache`` to
``/dev/shm/cf-cache``. Afterwards, the Java command should look like this::

    #!/usr/bin/env bash
    nice -n 19 java -cp "..." de.huberlin.wbi.cuneiform.cmdline.main.Main -l /dev/shm/cf-cache $@
    
Cuneiform will now run in-memory, never exceeding its preset memory limit.
