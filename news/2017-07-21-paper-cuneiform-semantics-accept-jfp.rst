Cuneiform Semantics Paper Accepted at Journal of Functional Programming
=======================================================================

2017-07-21

Our paper has been accepted at the Journal of Functional Programming and will be part of a Big data special issue.

Our `Cuneiform semantics paper <https://www.cambridge.org/core/journals/journal-of-functional-programming/article/computation-semantics-of-the-functional-scientific-workflow-language-cuneiform/1A3B8AB825939117C5BD9F850F63ADCC>`_ is available online in the Journal of Functional Programming volume 27, 2017.

Computation Semantics of the Functional Scientific Workflow Language Cuneiform
------------------------------------------------------------------------------

Cuneiform is a minimal functional programming language for large-scale scientific data analysis. Implementing a strict black-box view on external operators and data it allows the direct embedding of code in a variety of external languages like Python or R, provides data-parallel higher-order operators for processing large partitioned data sets, allows conditionals and general recursion, and has a naturally parallelizable evaluation strategy suitable for multi-core servers and distributed execution environments like Hadoop, HTCondor, or distributed Erlang. Cuneiform has been applied in several data-intensive research areas including remote sensing, machine learning, and bioinformatics, all of which critically depend on the flexible assembly of pre-existing tools and libraries written in different languages into complex pipelines.

This paper introduces the computation semantics for Cuneiform. It presents Cuneiform’s abstract syntax, a simple type system, and the semantics of evaluation. Providing an unambiguous specification of the behavior of Cuneiform eases the implementation of interpreters which we showcase by providing a concise reference implementation in Erlang. The similarity of Cuneiform’s syntax to the simply typed lambda calculus puts Cuneiform in perspective and allows a straight-forward discussion of its design in the context of functional programming. Moreover, the simple type system allows the deduction of the language’s safety up to black-box operators. Lastly, the formulation of the semantics also permits the verification of compilers to and from other workflow languages.