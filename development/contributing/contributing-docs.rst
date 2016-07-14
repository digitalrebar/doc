.. index::
  pair: Contributing; Docs

.. _contributing_docs:

Contributing Docs
-----------------

As always, please, follow the basic git setup to start, :ref:`contrib_basic`.

Edit Documentation
~~~~~~~~~~~~~~~~~~

We *love* Docs changes!

Docs may be edited directly from a fork on Githib, and therefore do not require local clones!  Changes can be directly installed by sending a pull request using Github where they will be approved and then added.  This method is great for simple changes; however, more complex changes require more examination and thought.


Cross References
~~~~~~~~~~~~~~~~

Please use Cross Reference ``.. _foo:`` and Index tags ``.. index::`` at the top of pages.  This helps build a complete guide.
 
Bigger Doc Changes
~~~~~~~~~~~~~~~~~~

For bigger doc changes, it is help to make a local environment to visualize the
modifications.  This helps make a consistent multi-page change and enables the user to acertain the impact of his or her changes.

The docs are automatically generated upon a successful pull request merge by the
read-the-docs system.  Sphinx builders to generate html and pdf docs.  At a minimum please validate the html doc as this reduces errors and smooths integration of new content. 

In order to validate the docs, a prerequisite environemnt is needed. 

On Linux/Mac
++++++++++++

`Sphinx <http://www.sphinx-doc.org/en/stable/install.html>`_. is required to create the environment in which docs can be built. 
For OS X 10.11, ``pip install sphinx`` is sufficient to create the required environment.

With that in place, ``make html`` will create a _build/html directory that contains the built files.
Using a browser pointed to the ``file://<working_dir>/_build/html/BOOK.html`` should allow the verification of the changes.

An additional tip is to run ``make html`` repeatedly in another terminal to capture changes as they are created. ::

  while [ true ] ; do
    make html
    sleep 1
  done


On Windows
++++++++++ 




To setup the environment, `Sphinx <http://www.sphinx-doc.org/en/stable/install.html>`_ is required, which requires installing `Python <https://www.python.org/downloads/>`_ and `pip <https://bootstrap.pypa.io/get-pip.py>`_.

With the environemnt created, ``sphinx-build -b html -d _build\doctrees . _build\html`` will build the files.  Using a browser pointed to ``C://<workinf dir>/_build/html/BOOK.html`` should allow verification of the changes. 

An additional tip is to run the builder repeatedly in a batch file or command terminal to capture changes as they are created.  ::

  cd path/to/clone
  :label
  echo building sphinx
  sphinx-build -b html -d _build\doctrees . _build\html
  timeout 1 >nul
  goto label

Doumentation Expectations
~~~~~~~~~~~~~~~~~~~~~~~~~

Documentation is an integral and formal component to the development process.  All documentation should be free from spelling and gramatical errors.   Additionally all documentation must adhere to a certain stylistic guide.

 1. All sentences must be followed by two spaces "__" while words are seperated by the standard single space "_".

 2. Use primarily third person when writing documentation. First person is sometimes acceptable, but second person (you, your) is almost always not. 

 3. Break thoughts into easy to read chunks rather than creating long paragraphs.

 4. Be certain to use embeded links when referencing a specific page or program. 
