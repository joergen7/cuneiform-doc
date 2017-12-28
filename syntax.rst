Cuneiform Syntax Reference
==========================

This section gives a formal definition of the Cuneiform syntax. The entry point
of a Cuneiform program is the :ref:`syntax_script`.

All syntax diagrams have been generated using the
`Railroad Diagram Generator <http://www.bottlecaps.de/rr/ui>`_.

Complete Cuneiform syntax in EBNF::

    script       ::= stat*

    stat         ::= query
                   | assign
                   | defun
                   
    query        ::= compoundexpr ';'

    defun        ::= 'deftask' ID sign( '{' assign+ '}'
                                      | 'in' lang '*{' BODY '}*' )
    
    sign         ::= '(' param+ ':' inparam* ')'
    
    inparam      ::= param
                   | '[' name+ ']'
    
    param        ::= name
                   | '<' name '>'
                   
    name         ::= ID( '(' 'String' ')' | '(' 'File' ')' )?

    assign       ::= ID+ '=' compoundexpr ';'
    
    lang         ::= 'bash' | 'lisp' | 'matlab' | 'octave' | 'perl' | 'python'
                   | 'r' | 'java' | 'scala'   
    
    compoundexpr ::= 'nil'
                   | expr+
    
    expr         ::= ID
                   | INTLIT
                   | '"' STRLIT '"'
                   | cnd
                   | app
                   
    cnd          ::= 'if' compoundexpr 'then' compoundexpr 'else' compoundexpr 'end'
    
    app          ::= ID '(' ( binding ( ',' binding )* )? ')'
                   
    binding      ::= ID ':' compoundexpr
    
.. toctree::
   :maxdepth: 1

   syntax_app
   syntax_assign
   syntax_compoundexpr
   syntax_cnd
   syntax_param
   syntax_inparam
   syntax_lang
   syntax_query
   syntax_binding
   syntax_script
   syntax_expr
   syntax_stat
   syntax_defun
   syntax_sign
   syntax_name


