Digital Rebar Troubleshooting Tips
----------------------------------

Chef-Client Fails: cannot download Chef RPM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If the very first role applied to a new node fails, there are several
possible causes.

1. outbound network access is not working. Likely cause is that your
   squid proxy is not configured
2. set the http\_proxy (\`export http\_proxy="http://127.0.0.1:8123")
   and attempt to access google.com from the admin server
3. if that worked, try the same thing after ssh'ing to the node
4. you are missing the /tftboot/files path
5. this can be caused when you do not have the ISOs staged

No OS? Installing an OS, the TFTP Process
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TFTP provides the boot images for the operating system install.

You can inspect the TFTP information the admin node provides by looking
in the ``/tftpboot`` directories.

These directories contain the sledgehammer discovery, base OS install
images and specific instructions for each node in the
``/tftpboot/nodes`` directory.

If Rebar is not providing the right boot image, this is a good place to
start.
