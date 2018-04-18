# Requirements

## Prerequisites

Stoplight currently supports the following Linux distributions for on-premise installations:

* Ubuntu 16.04 LTS (x86_64)
* CentOS / RedHat Enterprise Linux 7 (x86_64)

A minimum of one server is required to run the Stoplight application, however,
for a production installation, we recommend at least four servers (excluding
monitoring and backup servers). The system specifications for each server can be
found below under each component.

### Docker Installations

For the recommended Docker-based installation path, the only application requirements are:

* [Docker CE](https://www.docker.com/) v18.00+

### RPM Installations

For RPM-based installations, the application requirements are:

* [NodeJS](https://nodejs.org/) v8.9.4
* [PostgreSQL](https://www.postgresql.org/) v9.6+ (optionally included with GitLab)
* [Redis](https://redis.io/) v2.8+ (optionally included with GitLab)

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

Please note that the above recommendations are entirely optional if your
organization already has a monitoring and alerting solution in place.
