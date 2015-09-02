BDD Tips and Tricks
~~~~~~~~~~~~~~~~~~~

Usefule Steps in the BDD\_Catchall Module
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The catchall module has some useful steps for special cases and
debugging code that did not fit in other places. In fact, the step
generator function is really a BDD catchall!

Here are some useful steps found is the BDD\_Catchall module:

-  HTTP Server Logging
-  *I mark the logs with "Mark"*: handy to mark the logs so you can find
   a failure

-  Time Lapse
-  *pause "Time" seconds to "Message"*: if you have a time dependant
   issue that you cannot fix the right way
-  *after", Time, "seconds*: same as pause
-  *after", Time, "minutes*: same as pause
-  *after", Time, "milliseconds*: same as pause

-  Logging
-  *I debug BDD*: dumps log information into the BDD stream the the
   debug level
-  *I "puts" BDD*: same as above but at puts
-  *I "[debug \| trace \| info \|... ]" BDD*: same as above but user
   chooses the level

-  Play with pass/fail
-  *I do nothing to "Text"*: does nothing
-  *I always pass*: does what it says
-  *I always fail*: does what it says


