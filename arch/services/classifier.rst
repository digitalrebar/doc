.. index::
  pair: Services; Classifier
  pair: Container; Classifier

.. _arch_service_classifier:

Classifier
----------

The Classifier is a go-based program that processes a rules file. The file directs the Classifier to register with the Rebar API
event endpoint, processes those events, and takes action when events match the rules.  A system can have
multiple classifiers to enable system and user-based classifiers.

The deployment-based startup scripts will look for classifier files and start the appropriate number of classifiers.
