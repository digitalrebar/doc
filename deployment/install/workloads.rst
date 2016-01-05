Workloads Installer
===================

The ``workloads/[scripts]`` provide a complete system setup for a variety of workloads.  They are designed as one command, multiple target deployment scripts.

The following workloads are available

* workloads/base.sh

Each workload provides specialized configuration choices based on the cluster it creates, use --help in each script for a complete list.

Important General Configuration Options:

* --deploy-admin=[packet|aws] chooses where the file lives
* --provider=[packet|aws|gce] chooses where the nodes will be created
* --access=HOST required for most deployments.  FORWARDER is used for dev systems.
* --admin-ip=[CIDR] if you are targeting an existing system
