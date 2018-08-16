Cuneiform Syntax Reference
==========================

This section gives a formal definition of the Cuneiform syntax. The entry point
of a Cuneiform program is the :ref:`syntax_script`.

All syntax diagrams have been generated using the
`Railroad Diagram Generator <http://www.bottlecaps.de/rr/ui>`_.

Complete Cuneiform syntax in EBNF::

    script       ::= statement+

    statement    ::= import
                   | define
                   | e ';'

    import       ::= 'import' "'...'" ';'

    define       ::= let-define
                   | fun-define

    let-define   ::= 'let' pattern '=' e ';'

    fun-define   ::= 'def' id '(' (id ':' type (',' id ':' type)* )? ')' '->' type
                     ( 'in' lang '*{ ... }*' | '{' define* e '}' )

    pattern      ::= id ':' type
                   | '<' id '=' pattern (',' id '=' pattern)* '>'

    lang         ::= 'Bash'
                   | 'Erlang'
                   | 'Java'
                   | 'Matlab'
                   | 'Octave'
                   | 'Perl'
                   | 'Python'
                   | 'R'
                   | 'Racket'

    type         ::= 'Str'
                   | 'File'
                   | 'Bool'
                   | fun-type
                   | list-type
                   | record-type


    fun-type     ::= ('Ntv' | 'Frn') '(' (id ':' type)* ')' '->' type

    list-type    ::= '[' type ']'

    record-type  ::= '<' id ':' type (',' id ':' type)* '>'

    e            ::= id
                   | id '(' id '=' e (',' id '=' e)* ')'
                   | '"..."'
                   | "'...'"
                   | boolean-e
                   | cond-e
                   | list-e
                   | for-e
                   | fold-e
                   | record-e
                   | proj-e
                   | error-e

    boolean-e    ::= 'true'
                   | 'false'
                   | '(' e '==' e ')'
                   | 'not' e
                   | '(' e 'and' e ')'
                   | '(' e 'or' e ')'
                   | 'isnil' e

    cond-e       ::= 'if' e 'then' define* e 'else' define* e 'end'

    list-e       ::= '[' (e (',' e)*)? ':' type ']'
                   | '(' e '>>' e ')'
                   | '(' e '+' e ')'

    for-e        ::= 'for' id ':' type '<-' e (',' id ':' type '<-' e)* do define* e ':' type 'end'

    fold-e       ::= 'fold' id ':' type '=' e ',' id ':' type '<-' e do define* e 'end'

    record-e     ::= '<' id '=' e (',' id '=' e)* '>'

    proj-e       ::= '(' e '|' id ')'

    error-e      ::= 'error' '"..."' ':' type
    

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


