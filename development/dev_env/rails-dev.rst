.. index::
	pair: Rails; Development

.. _dev_guide_dev_mode:

Setting Rails Development Mode
------------------------------

Digital Rebar does not use use RAILS_ENV=development in the traditional way because most of our testing is targeted at doing real provisioning work that requires the production system.

If development behavior is required (classes and views that refresh when code changes) then perform the following steps:

#. Deploy Digital Rebar in the normal way
#. From the host, create the ``dev.mode`` file in the digitalrebar home directory and restart the rebar_api contain

   ```touch ~/digitalrebar/dev.mode
   cd ~/digitalrebar/deploy/compose && docker-compose restart rebar_api
   ```

Rails configuration changes may be made to the ``core/rails/config/environments/production.rb`` file.  If a Pull Request to update code is made, please remember to exclude that file from the file list.