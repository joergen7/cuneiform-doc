Website Reboot
==============

2019-12-31

I have rebooted the Cuneiform Website to improve my publishing workflow and to accomodate for planned changes.

One reason for the reboot is that I grew uncomfortable with the Jekyll-based website because I found it hard working around Ruby's iffiness. Somehow my distribution's package manager apt, Ruby's package manager gem, and bundle disagreed about what software is on my system and in what version. I do not want to micro-manage Ruby dependencies anymore. There are other static site generators with a more convenient workflow.

The second reason for the reboot is that I want Cuneiform's website and its documentation to be generated from a single source. Until now, I had a Jekyll-based home page and a Sphinx-based documentation. Migrating everything to Sphinx allows me to build the whole website from a single source.

As a consequence, the site should have a more smooth navigation. But also, I have to redo a lot of the content. If there is something missing from the website, that you have relied on then I apologize. I am working to get the full content back up as soon as possible.