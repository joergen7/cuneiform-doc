Andrey Salomatin Interviews Me on Concurrency
=============================================

2016-02-29

Andrey Salomatin has interviewed me on concurrency.

Podcast: `Concurrency: CSP and Actors <https://soundcloud.com/podcastcode/2-concurrency-csp-actors>`_.

Host: `Andrey Salomatin <https://twitter.com/flpvsk>`_

Multithreading is not the only approach we use to deal with concurrency. Single-purpose processes is our next frontier. Processes, that don't have shared state. To coordinate, they pass messages to each other.

We can build complex concurrent systems using simple principles of CSP or Actors model. We break down programs into independent processes, each performing some specific job, talking to each other. How they talk to each is the point of contention here. That's where the differences between CSP and Actors arise.

