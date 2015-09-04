Contributing to Digital Rebar
-----------------------------

Before `submitting pull requests <https://help.github.com/articles/using-pull-requests>`_, please make sure you understand the Apache license. We consider submitting a pull to be accepting the project's license terms.

We are using this `style <http://nvie.com/posts/a-successful-git-branching-model/>`__
branching model. The main goal is not to develop in *master*, but on the
*develop* branch so that *master* is the latest validated code.
*develop* should be stable and tests should have been run against it,
but hasn't necessarily been regression tested for production release
stability. Feature branches are encouraged for shared work. Large
features requiring multiple items or multiple individual participation
can be created in the Digital Rebar repo. This should be discussed in
the weekly Digital Rebar meetings. Once complete, these features would
be merged into *develop*.

Guidelines for Pull Requests
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  Must be Apache 2 license
-  For bugs & minor items (20ish lines), we can accept the request at
   our discretion
-  UI strings are localized (only EN file needs to be updated)
-  Does not inject vendor information (Name or Product) into Digital
   Rebar expect where relevant to explain utility of push (e.g.: help
   documentation & descriptions).
-  Passes code review by Digital Rebar team reviewer
-  Does not degrade the security model of the product
-  Items requiring more scrutiny

   -  Major changes
   -  New barclamps
   -  New technology

-  Pull requests should be against a defined feature branch in the
   Digital Rebar repo or the *develop* branch
-  Pull requests once pulled into *develop* will be merged into *master*
   at release boundaries.

Timing
^^^^^^

-  Accept no non-bug fix push requests within 2 weeks of a release fork
-  No SLA - code accepted at PTLs discretion. No commitment to accept
   changes.

Coding Expectations
^^^^^^^^^^^^^^^^^^^

-  Copyright & License header will be included in files that can
   tolerate headers
-  At least 1 line comments as header for all methods
-  Unit tests for all models concurrent with pull request
-  Tests for all API calls and web pages concurrent with pull
   request
-  Documentation for API calls concurrent with pull request
-  Adhere to the community [Ruby style guide]
   (https://github.com/bbatsov/ruby-style-guide)
-  Adhere to the community [Rails style guide]
   (https://github.com/bbatsov/rails-style-guide/)

Testing/ Validation
^^^^^^^^^^^^^^^^^^^

-  For core functions, push will be validated to NOT break build or
   deploy or our commercial products
-  For operating systems that are non-core, we will *not* validate on
   the target OS for the push 
-  Eventually, we would expect that a pull request would be built and
   tested in our CI system before the push can be accepted ' ####
   Feature Progression
