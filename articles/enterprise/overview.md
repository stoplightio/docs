# Stoplight Enterprise

The Stoplight Enterprise platform provides a fully-functional on-premise API
design, test, and documentation tool-kit, taking the hassle out of your API
strategy.

## Deployment Options

Stoplight can be deployed on one or many Linux servers (dedicated or
virtualized).

### Single-Server

Single-server deployments run all of the necessary Stoplight components on a
single Linux instance. This greatly simplifies the deployment process, as all
components do not have to reach over the network to talk to one another.

Despite ease of installation, there are some notable shortcomings to this
option:

* If the system is taken down for any reason, all components will be
  unavailable.

* Any single component can affect the performance of the entire Stoplight
  platform, leading to service degradation across all components.

Due to these shortcomings, single-server deployments are only recommended for
POC, pilot, or trial environments.

### Multi-Server

Multi-server deployments run different Stoplight Enterprise components on
separate Linux instances. This deployment option is much more resilient to
system-level issues, though it does require more network configuration.

Stoplight recommends multi-server deployments for all production installations.

### Native vs. Container-based Deployments

The Stoplight platform can be run either with a container solution (Docker) or
natively on the Linux system via RPM package installation. Both options are
fully supported, however Stoplight recommends leveraging containers where
possible for ease-of-use and improved security/sandboxing.

## System Requirements

Stoplight currently supports the following Linux distributions for on-premise installations:

* Ubuntu 16.04 LTS (x86_64)
* CentOS / RedHat Enterprise Linux 7 (x86_64)

A minimum of one server is required to run the Stoplight application, however,
for a production installation, we recommend at least four servers (excluding
monitoring and backup servers). The system specifications for each server can be
found below under each component.

### Docker Installations

For the recommended Docker-based installation path, Stoplight recommends [Docker
CE](https://www.docker.com/) v18.00+.

### RPM Installations

For RPM-based installations, the application requirements vary by component and
are addressed in the component pages referenced below.

## Stoplight Components

![](https://s3.amazonaws.com/user-content.stoplight.io/1564/1520952929100)

The Stoplight platform is broken up in to seven main components:

1.  [Stoplight App](/enterprise/components/app)
2.  [Stoplight API](/enterprise/components/api)
3.  [Stoplight Exporter](/enterprise/components/exporter)
4.  [Prism](/enterprise/components/prism)
5.  [Tasker (Jobs Server)](/enterprise/components/tasker)
    * [Hub Builder](/enterprise/components/hub-builder)
6.  [Pubs (Hubs Server)](/enterprise/components/pubs)
7.  [GitLab CE - Stoplight Fork](/enterprise/components/gitlab)

Please review each of the component pages prior to the installation.

## Monitoring

For monitoring purposes, Stoplight runs and recommends the following
applications:

* [InfluxDB](https://www.influxdata.com/time-series-platform/influxdb/) v1.3
  for metrics storage and aggregation
* [Kapacitor](https://www.influxdata.com/time-series-platform/kapacitor/) v1.3
  for alerting and metrics processing
* [Telegraf](https://www.influxdata.com/time-series-platform/telegraf/) v1.4
  for metrics collection
* [Mtail](https://github.com/google/mtail) v3.0 for whitebox monitoring of
  application logs

> Please note that the above recommendations are entirely optional if your
> organization already has a monitoring and alerting solution in place.
