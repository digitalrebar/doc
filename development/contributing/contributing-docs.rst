Contributing Docs
-----------------

As always, please, follow the basic git setup to start, :ref:`contrib_basic`.

Edit Documentation
~~~~~~~~~~~~~~~~~~

We *love* Docs changes!

You do NOT need a local clone to update docs! You can edit them right
from your fork on Github. Just make the changes and then create a pull
request using the Github UI.  This is great for simple changes.

Bigger Doc Changes
~~~~~~~~~~~~~~~~~~

For bigger doc changes, it is help to make a local environment to visualize your
modifications.  This helps make a consistent multi-page change and lets you test
your changes.

The docs are automatically generated upon a successful pull request merge by the
read-the-docs system.  We use Sphinx builders to generate html and pdf docs.  We 
would love for you to validate the html docs at a minimum before submitting a 
change.

To setup an environment, you will need to install `Sphinx <http://www.sphinx-doc.org/en/stable/install.html>`_.
For OS X 10.11, ``pip install sphinx`` was sufficient to build the docs.  The install link has methods for many platforms.

With that in place, ``make html`` will create a _build/html directory that contains the built files.
Using a browser pointed to the ``file://<working_dir>/_build/html/BOOK.html`` should allow you to verify changes.

An additional tip is to run ``make html`` in a one second loop in another terminal to pick up changes as you make them. ::

  while [ true ] ; do
    make html
    sleep 1
  done


