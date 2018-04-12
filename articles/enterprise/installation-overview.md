# Installation Overview

The Stoplight Enterprise platform provides a fully-functional on-premise API
design, test, and documentation toolkit, taking the hassle out of your API
strategy.

## Deployment Options

Before beginning with the installation, be sure to prepare all of the necessary
systems that will be running Stoplight components. For more information on
sizing, disk, and network requirements, please see the **Technical
Requirements** section.

### Single-server vs. Multi-server Deployments

Stoplight can be deployed on one or many Linux servers (dedicated or
virtualized). Single-server deployments run all of the necessary Stoplight
components on a single Linux instance. This greatly simplifies the deployment
process, as all components do not have to reach over the network to talk to one
another. Despite ease of installation, there are some notable shortcomings to
this option:

* If the system is taken down for any reason, all components will be
  unavailable.

* Any single component can affect the performance of the entire Stoplight
  platform, leading to service degradation across all components.

Due to the shortcomings listed above, single-server deployments are typically
recommended for POC/trial environments or for smaller organizations that do not
wish to allocate multiple servers for the Stoplight platform.

Multi-server deployments run different Stoplight Enterprise components on
separate Linux instances. This deployment option is much more resilient to
system-level issues, though it does require more network configuration.

> Stoplight recommends multi-server deployments for all production environments.

### Native vs. Container-based Deployments

The Stoplight platform can be run either with a container solution (Docker) or
natively on the Linux system. Both options are supported, however Stoplight
recommends leveraging containers where possible for ease-of-use and improved
security/sandboxing.
