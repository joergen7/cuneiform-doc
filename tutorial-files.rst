Files and Lists
===============

Learning Objective
  This tutorial deepens your understanding of Cuneiform's type system and how to use files.
  
  
Difficulty
  Basic
  
Duration
  30 min
  
Prerequisites
  Basic experience with Cuneiform (see :ref:`tutorial_basics`).
  
  
Introduction
------------

This tutorial is about handling files in Cuneiform. Files are a common way for scientific tools and libraries to exchange data. Cuneiform distinguishes filenames from strings (or Booleans) by associating filenames with a distinct type ``File``.


Explanation and Examples
------------------------

When it comes to files, Cuneiform has a black-box data model. I.e., Cuneiform has no knowledge about the data format of files. This has the advantage that Cuneiform foreign functions can exchange any kind of binary data format, e.g., compressed files. The disadvantage is that common operations like data partitioning cannot be performed implicitly, but need to be an explicit part of the program.

Types
^^^^^

In the :ref:`tutorial-basics` tutorial you have learned how to define and call
tasks. You may have noted that neither the input parameters nor the outputs had
any type information attached. In fact, there is a default type: `String`, which
is assumed when no further type information is given. Our `add` task in
:ref:`Example e-1.5 <e-1-5>`, when written with explicit type information, looks
like this:

Example e-2.1::
        
    deftask add( c( String ) : a( String ) b( String ) )in perl *{
      $c = $a+$b
    }*
    
Cuneiform's type system is rudimentary compared to the type systems you may know
from other languages. In fact, Cuneiform possesses only two types:

- String
- File

In the following section, we have a closer look at how to work with files.

The File Type
^^^^^^^^^^^^^

We can mark a task's input parameter to be a file by attaching the `File` type
to the parameter. A simple task using files may be a task outputing a single
file with a given content. 

Example e-2.2::
        
    deftask to-file( out( File ) : content )in bash *{
      out=out.txt
      echo $content > $out
    }*
    
    to-file( content: "Hello world" ); 
        
The task `hello` has one output parameter `out` of type `File` and one input
parameter `content` of the default type `String`. Calling this task with the
argument `"Hello world"` returns a file with the content `"Hello world"`.
Entering the above example in the Cuneiform interactive shell should look like
this::
        
        
    > to-file( content: "Hello world" ); 
    "4_out.txt"
    
.. hint::
   You find the output files produced by Cuneiform in the repo directory of the
   local Cuneiform cache. The location of the cache depends on your setup. If
   you installed Cuneiform with the :ref:`setup_chef_local`, the repo directory
   is located in `/tmp/cf-cache/repo`.


Mapping Over Lists
^^^^^^^^^^^^^^^^^^

Mapping a task over a list is the default behavior if a task is applied to a
list. If we, e.g., apply the previously defined task `to-file` to a list of
strings instead of a single string, the result is a list of files each
corresponding to an output

Example e-2.3::

    contentlist = "Hello world" "Goodnight moon";
    to-file( content: contentlist );

The application of the task `to-file` to the two-element list `content-list`
produces two files each with their respective content.

Processing a List as a Whole
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Sometimes the default behavior which maps a task over each element of a list is
not the desired behavior. Instead, a foreign task might need to consume a list
as a whole to perform some aggregation over its elements. To override the
default behavior and tell a task not to map over a list but to hand it to the
consuming task unaltered, we enclose the input parameter with angle brackets
`<>` in the task signature.

Example e-2.4::

    deftask cat( out( File ) : <file( File )> )in bash *{
      out=out.txt
      cat ${file[@]} > $out
    }*
    
    contentlist = "Hello world" "Goodnight moon";
    filelist = to-file( content: contentlist );
    
    cat( file: filelist );

The task `cat` has one input parameter `file` and one output parameter `out`
both being files. If the input parameter `file` is bound to a list, the task is
not mapped to each element of the list but the whole list is consumed by a
single application of cat. The body, which is written in Bash, concatenates all
files in the list. Let's try out the task `cat` by providing it two files. The
output of this workflow is a single file with two lines::
	
    Hello world
    Goodnight moon
    
Tasks producing lists
^^^^^^^^^^^^^^^^^^^^^

In some cases, we need to define tasks that output a list. We can specify an
output to be a list in the same way we did with the input: by enclosing the
output parameter in angle brackets `<>`.

Example e-2.5::
	
    deftask split4( <out( File )> : file( File ) )in bash *{
      split -d -l 4 -a 6 $file out.
      out=out.*
    }*
    
    file = cat( file: to-file( content: 1 2 3 4 5 6 7 8 ) );
    filelist = split4( file: file );
    
    filelist;

The task `split4` takes a file and partitions it. A new partition is
generated for every four lines in the input file. A list of files is returned
enumerating the partitions. When we apply `split4` to a file containing 8 lines,
2 output files are produced which are stored in the variable `filelist`.


Assignments
-----------

Assignment a-2.1
^^^^^^^^^^^^^^^^

How many files are produced when applying the task `split4` to a list
with two files, each containing 8 lines? Test your answer in the Cuneiform
interactive shell.

Assignment a-2.2
^^^^^^^^^^^^^^^^

Define a task `to-string` which takes a file and returns its content as a
string. Test the task in the Cuneiform interactive shell. Use it on a list of
files.

Assignment a-2.3
^^^^^^^^^^^^^^^^

Define a workflow which consumes a text file. The workflow partitions the file
one line for each partition and counts the words in each line. The resulting
word counts are added in a third step.


Solutions
---------

Solution a-2.1
^^^^^^^^^^^^^^^^

Each 8-line file produces 2 output files. Since the split task is called for
each of the two files, the output set contains 4 files.
    
Solution a-2.2
^^^^^^^^^^^^^^^^

::
	
    deftask to-string( out : file( File ) )in bash *{
      out=`cat $file`
    }*

Solution a-2.3
^^^^^^^^^^^^^^^^

::
	
    deftask to-file( out( File ) : content )in bash *{
      out=out.txt
      echo $content > $out
    }*

    deftask cat( out( File ) : <file( File )> )in bash *{
      out=out.txt
      cat ${file[@]} > $out
    }*

    deftask split( <out( File )> : file( File ) )in bash *{
      split -d -l 1 -a 6 $file out.
      out=out.*
    }*

    deftask wc( n : file( File ) )in bash *{
      n=`wc -w $file | awk {'print $1'}`
    }*
    
    deftask sum( s : <n> )in perl *{
      $s = eval join '+', @n;
    }*
    
    contentlist = "if thou"
                  "must love me"
                  "let it"
                  "be"
                  "for nought";
    
    file = cat( file: to-file( content: contentlist ) );
    
    partitionlist = split( file: file );
    countlist = wc( file: partitionlist );
    s = sum( n: countlist );
    
    s;

