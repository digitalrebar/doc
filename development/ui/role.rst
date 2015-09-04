Barclamp Roles - User Interface Development and Testing
-------------------------------------------------------

When a deployment role is in proposed state the user should be able to
modify the role attributes defined for that role.

In all other states the attributes should be displayed as read-only.
Please use the Messaging Barclamp as a reference and this guide for
developing and testing other custom role user interfaces.

Development
~~~~~~~~~~~

The steps for building the UI (view) to edit and display node role
attributes are as follows

1. Define the attributes for the Role in the Barclamp's rebar.yml if
   they are not already present. These definitions will create Attrib
   objects for the Role in Rebar.

   Sample attributes: \`\`\`yaml roles:

-  name: messaging-server jig: chef-solo requires:

   -  openstack-base attribs: # name used as id field in haml input
      tags. Needs to follow this convention:
      [barclamp]-[role]*rest*\ of\_id

      -  name: 'messaging-openstack\_endpoints\_mq\_host' # Plain
         English description of attrib description: 'Messaging Host' #
         map to value in hash:
         hsh['openstack']['endpoints']['mq']['host'] for example map:
         'openstack/endpoints/mq/host'
      -  name: 'messaging-openstack\_endpoints\_mq\_port' description:
         'Messaging Port' map: 'openstack/endpoints/mq/port'
      -  name: 'messaging-rebar\_messaging\_mq\_user' description:
         'Messaging User' map: 'rebar\_messaging/mq/user'
      -  name: 'messaging-rebar\_messaging\_mq\_password' description:
         'Messaging Password' map: 'rebar\_messaging/mq/password' \`\`\`

2. Create the view for the role

   Rebar expects the view file location and name to follow the
   convention:

   ::

       [barclamp_name]/rebar_engine/barclamp_[barclamp_name]/app/views/barclamp_[barclamp_name]/node_roles/_[@role.name].html.haml

   For the messaging server role the following Rails partial was
   created:

   ::

       messaging/rebar_engine/barclamp_messaging/app/views/barclamp_messaging/node_roles/_messaging-server.name.html.haml

   The partial is made up of four main components, the form, the
   validation rules, the validation messages and the read-only view. The
   template for the overall partial should follow this pattern:

\`\`\`haml - data\_nil\_empty = (data.nil? \|\| data=={}) - if
@node\_role.proposed? # The node role can be edited in this state, show
the form %dl.attribs %dt= t('.[label\_key]') %dd= text\_field\_tag
'data\_[@role.name]\ *[map\_to\_value]', (data*\ nil\_empty \|\|
data["map"]["to"]["value"].nil?) ? template["map"]["to"]["value"] :
data["map"]["to"]["value"] , :size => 30 ... = hidden\_field\_tag
:dataprefix, "data\_"

::

    :javascript
      var rules = new Array();
      // cannot use regular json syntax because you cannot have hyphen in key names and attribs have hyphen, TODO should re-factor attribs to use json friendly key names
      rules["data_[@role.name]_[map_to_value]"] = new Object({
        required: true,
        minlength: 8
        //... 
      });
      //... 
      var messages = new Array();
      messages["data_[@role.name]_[map_to_value]"] = new Object({
        required: "#{t('.[field_label_required]', size: 8)}"
        //... 
      });
      //..

-  else # Not in proposed state, show read-only page. %dl.attribs %dt=
   t('.[label\_key]') %dd= (data\_nil\_empty) ?
   template["map"]["to"]["value"] : data["map"]["to"]["value"] ...
   \`\`\`
-  *IMPORTANT*: The ids used in the form fields *MUST* match the ids
   used to build the rules and messages javascript arrays.

3. Add localization for all labels and validation messages. This follows
   the conventions mentioned in the `localization <localization.md>`__
   documentation and the general localization pattern for the view above
   is as follows:

   ::

       en:
         barclamp_[barclamp_name]:
           node_roles:
             [role_name]:
               label_key: Label Value
               message_key: Message with parameter: %{parameter}

4. Override Role hooks if needed

   If any special actions need to take place prior to sending the data
   down to the node after the Deployment is committed you can override
   one of the hooks declared in
   `Role <https://github.com/rebar/barclamp-rebar/blob/master/rebar_framework/app/models/role.rb>`__.

   For example in the messaging barclamp an encrypted databag needs to
   be created on the admin node populated with the user and password
   from the form. The data bag is then copied downstream to the node
   prior to a chef run.

   Create a class that extends Role and use the following name/location
   convention:

   ::

       class Barclamp[Role::Name} < BarclampChef::Role

       [barclamp_name]/rebar_engine/barclamp_[barclamp_name]/app/models/barclamp_[barclamp_name]/[role_name].rb

   For example, in the messaging barclamp the class used for the server
   role hook override is:

   ::

       class BarclampMessaging::Server < BarclampChef::Role

       messaging/rebar_engine/barclamp_messaging/app/models/barclamp_messaging/server.rb

   The hook override used in the encrypted data bag use case is the
   *on\_todo* hook which is called when the node role is moved into the
   to\_do state once all, if any, blocking parent roles make it to
   active state, but before the data is pushed down to the target node,
   so this hook is ideal for this use case. Sample code from Messaging
   Barclamp below:

   .. code:: ruby

       def on_todo(node_role, *args)
          nrd= node_role.data
          if(!nrd.nil? && nrd != {} && !nrd["rebar_messaging"]["mq"]["user"].nil? \
          && !nrd["rebar_messaging"]["mq"]["password"].nil?)
         messaging_user_id = nrd["rebar_messaging"]["mq"]["user"]
         messaging_password = nrd["rebar_messaging"]["mq"]["password"]
         store_credential( "messaging", "user", messaging_user_id, messaging_password)
       end
         end

Testing
~~~~~~~

A typical front-to-back testing scenario is outlined below, using the
Messaging Barclamp as an example:

1.  Start the Admin node, log in and create new Deployment.
2.  Start a new test node, either a VM or actual hardware.
3.  Validate the test node has PXE booted and is the discovered state in
    the UI
4.  Create a new Deployment and add the single role you are trying to
    test, messaging-server for example.
5.  Add the newly discovered node to the Deployment
6.  At the intersection of the role and node click the green + icon to
    expand all the parent roles.
7.  At this point the very last role, from left-to-right, should be the
    role you are testing with a blue diamond icon at the intersection of
    the node and role. The blue diamond indicates the node role is in
    the Proposed state. Click this icon, this will bring you to the Node
    Role view that contains the functionality you are testing.
8.  Before proceeding copy the ID of the node role you are editing to be
    used later on. This can be found by looking at the URL of the page.
    For instance the following
    http://192.168.124.10:3000/node\_roles/84, shows that the node role
    is 84
9.  Validate the form fields and labels are correct that the form
    validation is working properly. Validation error messages should be
    displayed to the right of the field in question. In order to
    validate the rules the tester should know what each field's validation rules are supposed to be.
10. Test required fields by clearing them all and attempt to save the
    node role. You should see required messages for every field in the
    messaging server role for example as every field is required
11. Validate and field length rules are working correctly, there are
    on-key-up event handlers on each field and when the length doesn't
    meet the defined max/min length, you should be notified.
12. Validate special case fields like password and email. In messaging
    there is a custom validator defined that will not allow special
    characters in the password. If you enter % you should see a
    validation error message.
13. Enter all required information in the correct format and save the
    node role. You should see a notification in the standard global
    notification section of the page that the node role has been saved
    successfully.
14. Navigate through the deployments menu to get back to the deployment
    node role list page again. Click the blue icon for the role you are
    testing and validate the information you previously changed. This action will
    repopulate the form.
15. Make additional changes and repeat previous step to validate the
    additional update was successful. The reason for this is the first
    time you edited the node role you were overwriting the defaults,
    creating a new object. This second pass is an update of that object.
16. Testing of the rendered form is done at this point. It may be
    worthwhile to validate model data itself is correct prior to
    committing the deployment. This can be easily done through the Rails
    console:
17. SSH into the admin node navigate to the rebar\_framework director
    ``:~$ cd /opt/dell/rebar_framework``
18. Start the rails console
    ``:~$ RAILS_ENV=development bundle exec rails c``
19. Use the Rails console to retrieve the node role object
    ``irb(main):001:0> nr = NodeRole.find(84)``
20. Verify the model matches the changes made in UI
    ``irb(main):001:0> y nr.data # This prints out a yaml version of the data that was modified in the UI``
    It should look something like:

    .. code:: yaml

          openstack:
            endpoints:
              mq:
                port: 5532
                host: 127.0.0.1
            rebar_messaging:
              mq:
                user: the_user
                password: the_password

21. If the information looks correct in the model commit of the Deployment
    UI. While the parent node is executing, such as
    installing the operating system etc, you can take a look at the
    read-only node role view by clicking the grey circle icon
    (indicating blocked state) at the intersection of the node and role.
    This will take you to the read-only node role view. Validate the
    fields and data correct.
22. When the Deployment is finished and active, the last step is to
    verify the settings in the UI actually made it to the target
    node and configured the service correctly. The validation steps will
    be different for each role. For the Messaging Server role the
    following should be verified:
23. SSH into the target node and verify that the service is running
    ``:~$ sudo rabbitmqctl status``
24. Verify the settings are correct in the RabbitMQ config and
    environment files
    ``:~$ sudo less /etc/rabbitmq/rabbitmq.config   :~$ sudo less /etc/rabbitmq/rabbitmq-env.conf``
25. This completes testing and verification of the entire life-cyle,
    from the UI to the actual deployed service.


