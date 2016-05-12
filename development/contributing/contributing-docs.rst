Contributing Docs
-----------------

Fork The Code
~~~~~~~~~~~~~

    we assume you already have a clone of
    ``https://github.com/digitalrebar/doc``

1. create a personal fork of the
   ``https://github.com/digitalrebar/doc``

   1. Fork the code if you want to be able to submit changes
   2. rename your fork in Github to something like 'rebar-doc' to make
      it easier to track. We'll assume that you did that in these
      directions
   3. remember to update your public SSH key to github

2. setup your git identity (one time only)

   1. ``git config --global user.name "user.name"``
   2. ``git config --global user.email "email.address"``

3. add a personal remote:
   ``git remote add personal`` https://github.com/[yourgitnamehere]/[rebar-doc]\`
4. you can check your remotes using ``git remote -v``
5. get the latest code from your repo ``git fetch personal``

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


To Create a Pull Request
~~~~~~~~~~~~~~~~~~~~~~~~

1. make your change and commit it:
   ``git commit -a -m "I cut and pasted this"``
2. get the latest code from origin: ``git fetch``
3. sync your code into the trunk: ``git rebase``

   1. you may have to merge changes using
      ``git add [file]= and =git rebase --continue--``

5. push your change to your personal repo in a branch:
   ``git push personal master:[my-pull-request-branch]``
6. from your Github fork UI, create a pull request from
   my-pull-request-branch

Work On a Branch
~~~~~~~~~~~~~~~~

It's good practice to work on a branch instead of trunk. That allows you
to isolate several changes into distinct pulls instead of co-mingling
changes.

1. get on master using 'git checkout master'
2. make sure you are up to date using ``git fetch`` and ``git rebase``
3. create a branch using ``git branch [namehere]``
4. switch to that branch using ``git checkout [namehere]``
5. work & commit
6. when you are ready to push, use
   ``git push personal [namehere]:[namehere]``

You can switch between branches anytime! That allows you to help on
master or work on multiple pull requests. This flow is especially handy
if your pull may take a few days to be accepted because you can work on
your next item while the community does the review. It also isolates you
from changes in master. If you need to get changes from master, use
``git merge master`` from your branch.

