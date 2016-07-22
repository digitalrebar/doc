

Overview//TBD//
===============

At Digital Rebar, we not only strive to provide excellent deployment services, but an excellent user experience.  In order to satisfy that imperative, we have developed a new user interface.  
The new interface provides a sleek new way to interact with server deployment, and has been designed with efficiency in mind.  


General
-------

Upon logging in, the user interface will open to the Deployments page. The top of every page is dominated by this header:

.. image:: /images/screens/webux/overview.png


The name of the selected page is posted on the left, while the tenant is displayed to the right.  
The two icons are for refreshing data and viewing the annealer respectively. Thanks to the data refresher, users should not need to refresh the page. 

The Annealer
~~~~~~~~~~~~

When opened, the Annealer shows the progress of node role deployment. 


.. image:: /images/screens/webux/annealer.png


* Error shows all of the node roles in error.  
* Process shows all of the node roles which are being processed.  
* Todo shows nodes that are about to be processed.  
* Queue shows nodes that are waiting to enter Todo.  

**Note:** Error has a retry button that will send all erroneous node roles back to the queue 


