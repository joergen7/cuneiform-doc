Erlang Foreign Function Interface (effi)
========================================

The Erlang foreign function interface (Effi) is a way to run code in arbitrary foreign languages, e.g., Python or Octave from a native (Erlang) environment.

Herein, the foreign code is executed in an environment that binds a defined set of input variables to values defined from the outside. After completion of the foreign code, a set of output variables is expected to be bound to values.

The foreign code snippet along with input variable bindings is given to effi in the form of a key-value map in a format that can easily be decoded/encoded using the `jsone <https://github.com/sile/jsone>`_ JSON serialization library. Accordingly, effi comes with a command-line application that reads and writes JSON files.

.. toctree::
   :maxdepth: 2

   effi_supported_languages
   effi_integration
   effi_synopsis
   effi_api
   effi_format
   effi_requirements