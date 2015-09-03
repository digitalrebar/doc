Development Server
==================

Dev/Simulator allows you to play with the UI and BDD tests which is
good for developers working on the UI/API and Annealer logic.

The Dev environment does not start all the services and cannot be used to provision nodes.  It is for UI/API development only because it picks up code changes immediately.

   1. Start with ``tools/docker-admin centos ./development.sh``
   #. Dev mode creates a special user ``developer/Cr0wbar!``
   #. To monitor the logs inside the container, use
      ``tail -f /var/log/rebar/development.log``
   #. Run the `BDD system <development/testing-bdd>`_
