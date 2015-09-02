Short Term notes for running the Digital Rebar in Docker
--------------------------------------------------------

This is the TL;DR version; the full version is
`here <docker-admin.md>`__.

1.  Place the OS install ISOs for OSes you want to deploy on to slaves
    in ``$HOME/.cache/digitalrebar/tftpboot/isos``. We currently
    support:
2.  ``CentOS-6.5-x86_64-bin-DVD1.iso``
3.  ``RHEL6.4-20130130.0-Server-x86_64-DVD1.iso``
4.  ``ubuntu-12.04.4-server-amd64.iso``
5.  Prep Environment
6.  Install Docker (do once)
7.  ``sudo chmod 666 /var/run/docker.sock`` (to run docker without sudo)
8.  ``sudo usermod -a -G docker <your-user>`` (to permanently run Docker
    without sudo)
9.  To build Sledgehammer:
10. ``tools/build_sledgehammer.sh``
    `Details <../../workflow/dev-build-sledgehammer.md>`__
11. To run in development mode:
12. ``tools/docker-admin centos ./development.sh``
13. To run in production mode:
14. ``tools/docker-admin centos ./production.sh admin.cluster.fqdn`` The
    first time you run this, it will take awhile as caches a few
    critical files and extracts the ISOs.
15. ``tools/kvm-slave`` (to launch a KVM-based compute node)

Once Rebar is bootstrapped (or if anything goes wrong), you will get a
shell running inside a 'tmux' session, the first of which is in the
container. Exiting the shell will kill Docker.

More about tmux:

http://tmuxp.readthedocs.org/en/latest/about\_tmux.html
