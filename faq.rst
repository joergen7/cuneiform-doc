FAQ
===

Frequently Asked Questions

**Why do another data flow language? Are there not enough languages already?**

Developers have conceived many data flow languages. The idea of programming with data flow is at least as old as `GNU Make <http://www.gnu.org/software/make/>`_. But the build systems that we know of fall short of the expressive power of functional programming languages. By contrast, functional programming languages don't focus enough on software integration and parallelization.

**Parallelizing functional programs were big in the 1980s but never caught on. How does Cuneiform add to what we already have?**

We can only speculate about the reasons for the success or failure of the software projects of the 1980s. In our opinion, parallel functional programming would be commonplace if clock rates had not `doubled every 18 months <https://en.wikipedia.org/wiki/Moore%27s_law>`_ for a long time. We can recover these ideas now that processor clock rates have remained mostly constant for a decade. Languages like Scala or Clojure are successful, in part, because many people understand that functional programming suits multi-processor systems. However, these languages, being general-purpose languages, are hybrids: some of their features are counter parallelism like mutable references or shared data structures. Cuneiform, being a special-purpose language, is focused: *all* of its features are easy to parallelize. And this special purpose approach is missing in programming languages available today.

**Why does Cuneiform not support Ruby/Clojure/Julia?**

We aim to integrate as many languages as we can. If you do not find your favorite language on the list consider contributing to make it compatible.

**Cuneiform is a student project and many students abandon their project after graduating. What's the guarantee that Cuneiform continues to develop?**

We will make all efforts to maintain Cuneiform in the future. Consider contributing or joining the team to help it grow!

**I understand the general idea behind Cuneiform, but can it be implemented?**

Currently, Cuneiform is in a beta stage of development, meaning that the most important features are implemented and that we keep the user interface (the language) stable. The package contains a Cuneiform interpreter and a distributed execution environment so we would argue that it has indeed been implemented.

**Distributed computing is a complex research topic, and scheduling or dealing with failures is hard. How can Cuneiform cover all these complexities?**

The way we deal with the complexities of distributed computing is twofold: (i) Many problems in this domain, like message passing or failure detection, are Erlang's turf. Erlang deals with them admirably and we simply make use of that. (ii) All other problems in this domain actually have quite simple solutions and Cuneiform implements them effectively.

**Cunei-what? How did you come up with that name?**

Programming languages are writing systems and Cuneiform is one of the oldest writing systems we know about. So the author thought it would be a fitting name for the least-old writing system around and was too ignorant of the fact that there is already an open source `OCR software <https://en.wikipedia.org/wiki/CuneiForm_(software)>`_ with the same name.

**I have always got my work done. Do I really need all this fancy-schmancy recursive higher-order heiopei?**

Which language features are useful depends on the use case. It could be that the use cases you deal with really do not depend on features only a functional programming language can offer. In this case, you might be happy with the workflow language you already use. If, however, your use cases do depend on such features it might still be possible that you can get your work done somehow. I would think you are in for an improvement though.

**There are other well-known systems with active communities. No one knows Cuneiform and a community is pretty much non-existent. Why would I do this to myself?**

We are aware that the risk profile of using Cuneiform is slightly higher than that of other software you can find out there, but we firmly believe that the effectiveness of the solutions it offers make Cuneiform the right choice for those working in genetic research. The support level is constantly growing and the software provides a proven way to process genetic data swiftly and robustly.