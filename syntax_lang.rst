.. _syntax_lang:

Language Id (lang)
==================

A Language Id (lang) can be any of the supported scripting languages.

A Language Id is part of a foreign :ref:`syntax_defun`.

**lang:**

.. image:: img/lang.png

::

    lang ::= 'bash' | 'lisp' | 'matlab' | 'octave' | 'perl' | 'python' | 'r' | 'java' | 'scala'   
    
.. warning::
   The Lisp support in the current Cuneiform version 2.0.2-SNAPSHOT is
   not functional. We will fix this shortly.
