BDD Config
^^^^^^^^^^

The BDD configuration file contains information that tells BDD how to
execute. While BDD adds to this file during execution, users choose
which values it starts with.

BDD selects the ``default.config`` file automatically. You can choose
which configuration to load by passing it into the ``bdd:test(config)``
or ``bdd:feature(config, feature)`` methods.

.. raw:: html

   <table>
     <tr>
       <th>

Item

.. raw:: html

   </th>
       <th>

Required

.. raw:: html

   </th>
       <th>

Default

.. raw:: html

   </th>
       <th>

Comment

.. raw:: html

   </th>
     </tr>
     <tr>
       <td>

url

.. raw:: html

   </td>
       <td>

yes

.. raw:: html

   </td>
       <td>

none

.. raw:: html

   </td>
       <td>

This is the URL that BDD will use for testing

.. raw:: html

   </td>
     </tr>
     <tr>
       <td>

user

.. raw:: html

   </td>
       <td>

no

.. raw:: html

   </td>
       <td>

none

.. raw:: html

   </td>
       <td>

If your site requires auth, then this is required

.. raw:: html

   </td>
     </tr>
     <tr>
       <td>

password

.. raw:: html

   </td>
       <td>

no

.. raw:: html

   </td>
       <td>

none

.. raw:: html

   </td>
       <td>

If your site requires auth, then this is required. WARNING: Retained in
clear text! Do not store production passwords here!

.. raw:: html

   </td>
     </tr>
     <tr>
       <td>

log

.. raw:: html

   </td>
       <td>

no

.. raw:: html

   </td>
       <td>

[true, puts, info, warn, error]

.. raw:: html

   </td>
       <td>

used by bdd\_utils:log printouts. Create list with none, some or all of
the following: [puts, trace, debug, info, warn]

.. raw:: html

   </td>
     </tr>
     <tr>
       <td>

titles

.. raw:: html

   </td>
       <td>

no

.. raw:: html

   </td>
       <td>

[pass, fail, skip, header, result, feature, step, step\_pass,
step\_fail]

.. raw:: html

   </td>
       <td>

used by bdd\_utils:log printouts.

.. raw:: html

   </td>
     </tr>
     <tr>
       <td>

environment

.. raw:: html

   </td>
       <td>

no

.. raw:: html

   </td>
       <td>

undefined

.. raw:: html

   </td>
       <td>

used by Unless step prefix to skip tests

.. raw:: html

   </td>
     </tr>
     <tr>
       <td>

results\_out

.. raw:: html

   </td>
       <td>

no

.. raw:: html

   </td>
       <td>

/tmp/bdd\_results.out

.. raw:: html

   </td>
       <td>

stores the detailed results of the tests. Used by bdd:failed().

.. raw:: html

   </td>
     </tr>
     <tr>
       <td>

coverage\_out

.. raw:: html

   </td>
       <td>

no

.. raw:: html

   </td>
       <td>

/tmp/bdd.html

.. raw:: html

   </td>
       <td>

HTML version of test results

.. raw:: html

   </td>
     </tr>
     <tr>
       <td>

marker\_url

.. raw:: html

   </td>
       <td>

no

.. raw:: html

   </td>
       <td>

undefined

.. raw:: html

   </td>
       <td>

If undefined, this behavior is turned off. If defined, BDD does a web
request to URL with debug information to make it easier to find matching
steps in the log. For Digital Rebar, the url is ``utils/marker``

.. raw:: html

   </td>
     </tr>
     <tr>
       <td>

marker\_log/td>

.. raw:: html

   <td>

no

.. raw:: html

   </td>
       <td>

/var/log/rebar/development.log

.. raw:: html

   </td>
       <td>

Should point to the path where you log API calls

.. raw:: html

   </td>
     </tr>
     <tr>
       <td>

cli

.. raw:: html

   </td>
       <td>

no

.. raw:: html

   </td>
       <td>

undefined

.. raw:: html

   </td>
       <td>

Used by bdd\_clirat for the command to the CLI if not in the given

.. raw:: html

   </td>
     </tr>
     <tr>
       <td>

cli\_user\_key

.. raw:: html

   </td>
       <td>

no

.. raw:: html

   </td>
       <td>

--username

.. raw:: html

   </td>
       <td>

Used by bdd\_clirat to pass the username into the CLI

.. raw:: html

   </td>
     </tr>
     <tr>
       <td>

cli\_password\_key

.. raw:: html

   </td>
       <td>

no

.. raw:: html

   </td>
       <td>

--password

.. raw:: html

   </td>
       <td>

Used by bdd\_clirat to pass the password into the CLI

.. raw:: html

   </td>
     </tr>
     <tr>
       <td>

cli\_url\_key

.. raw:: html

   </td>
       <td>

no

.. raw:: html

   </td>
       <td>

--url

.. raw:: html

   </td>
       <td>

Used by bdd\_clirat to pass the URL into the CLI

.. raw:: html

   </td>
     </tr>
     <tr>
       <td>

system\_phantom

.. raw:: html

   </td>
       <td>

no

.. raw:: html

   </td>
       <td>

system-phantom.internal.local

.. raw:: html

   </td>
       <td>

Used by Rebar to set the name of the phantom

.. raw:: html

   </td>
     </tr>
     <tr>
       <td>

system\_phantom\_roles

.. raw:: html

   </td>
       <td>

no

.. raw:: html

   </td>
       <td>

["dns-service", "ntp-service","dns-mgmt\_service"]

.. raw:: html

   </td>
       <td>

Used by Rebar to set the name of the phantom roles

.. raw:: html

   </td>
     </tr>
     <tr>
       <td>

consul\_url

.. raw:: html

   </td>
       <td>

no

.. raw:: html

   </td>
       <td>

http://127.0.0.1:8500

.. raw:: html

   </td>
       <td>

Used by Rebar to set the consul server location

.. raw:: html

   </td>
     </tr>

   </table>

Example Config
''''''''''''''

::

    %%-*-erlang-*- 
    {url, "http://192.168.124.10:3000"}.
    {user, "developer"}.
    {password,"Cr0wbar!"}.
    {feature_path,"features/"}.
    {extension, "feature"}.
    {global_setup, rebar}.
    {secondary_step_files, [rebar_rest, rebar, bdd_webrat, bdd_restrat, bdd_catchall]}.
    {translation_error, "translation_missing"}.

