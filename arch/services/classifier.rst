
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Services; Classifier
  pair: Container; Classifier

.. _arch_service_classifier:

Classifier
----------

The Classifier is a go-based program that processes a rules file. The file directs the Classifier to register with the :ref:`arch_service_rebar_api`
event endpoint, processes those events, and takes action when events match the rules.  A system can have
multiple classifiers to enable system and user-based classifiers.

The deployment-based startup scripts will look for classifier files and start the appropriate number of classifiers.
