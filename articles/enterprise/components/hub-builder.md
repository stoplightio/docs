# The Stoplight Hub Builder

The **Hub Builder** component converts a Stoplight Hub into a standalone static HTML website, suitable for viewing and distribution.

> #### Networking Details
>
> The Hub Builder does not have a listening service or external port configurations.

> #### Component Dependencies
>
> The Hub Builder is started in an ad-hoc manner by **Tasker**, and does not have
> any component dependencies.

## Installation

The Stoplight Hub Builder can be installed with Docker or via RPM package.

### RPM Package

Prior to installing the RPM package, you will need to:

* Install NodeJS

* Have the Stoplight package repository installed and configured with your user-specific credentials

#### Installing NodeJS

To install NodeJS, run the following commands:

```bash
# make sure all current versions of nodejs are removed
sudo yum remove nodejs npm -y

# install nodejs
sudo rpm -Uvh https://rpm.nodesource.com/pub_8.x/el/7/x86_64/nodejs-8.9.4-1nodesource.x86_64.rpm
```

Once the installation has completed, verify the version installed with the command:

```bash
$ node --version
v8.9.4
```

If you do not see a version starting `v8.9`, contact Stoplight support for assistance.

#### Setting up the Package Repository

You can do this by copying-and-pasting the contents below into a terminal:

```bash
# expose credentials to environment first
REPO_USERNAME="myusername"
REPO_PASSWORD="mypassword"

# write credentials to repo file
cat <<EOF | sudo tee /etc/yum.repos.d/stoplight.repo
[stoplight]
name=Stoplight Package Repository
baseurl=https://$REPO_USERNAME:$REPO_PASSWORD@pkg.stoplight.io/rpm
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://pkg.stoplight.io/stoplight.key
EOF
```

> Be sure to set your repository credentials before issuing the `cat` command

#### Installing the Hub Builder Package

Once the repository is configured properly, you can install the Hub Builder
component using the command:

```bash
sudo yum install stoplight-hub-builder -y
```

### Docker

To install the Hub Builder component with Docker, run the command below:

```bash
docker pull quay.io/stoplight/hub-builder
```

> Note, if you have not already authenticated with the Stoplight container
> registry, you will be prompted for credentials

## Configuration

The Hub Builder component is an ad-hoc processing job, and does not have any
required configuration that is not provided by the parent process (typically
Tasker).

## Running

## RPM Package

The Hub Builder component is an ad-hoc processing job, and does not have an
associated service. The Tasker component is responsible for running and managing
the Hub Builder jobs.

To ensure Tasker is able to run the Hub Builder package correctly, be sure to
set Tasker to `shell` mode in the Tasker configuration.

### Docker

The Hub Builder component is an ad-hoc processing job, and does not have an
associated service. The Tasker component is responsible for running and managing
the Hub Builder container.
