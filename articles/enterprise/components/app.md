# The Stoplight App

The **App** component powers the Stoplight user interface by connecting users to
the Stoplight API and other services. This is the primary point of ingress for
most users using Stoplight. It is what they will load in their web browser, and
connect the desktop app to.

> #### Networking Details
>
> The default port for the App component is TCP port **3100**. The port can be
> customized using the `PORT` configuration variable.
>
> The App must be able to receive **incoming** connections from the following components:
>
> * User Clients (web browser or desktop application)
>
> The App must be able to make **outgoing** connections to the following components:
>
> * API
> * Prism
> * Exporter

> #### Component Dependencies
>
> Make sure the following components are available **before** starting the App
> service:
>
> * API

## Installation

The Stoplight App can be installed with Docker or RPM package.

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

#### Installing the App Package

Once the repository is configured properly, you can install the app component using the command:

```bash
sudo yum install stoplight-app -y
```

### Docker

To install the app component with Docker, run the command below:

```bash
docker pull quay.io/stoplight/app
```

> Note, if you have not already authenticated with the Stoplight container registry, you will be prompted for credentials

## Configuration

To configure the Stoplight App component, you will need to provide connection
details to the other necessary Stoplight components. The API can be configured
either by the configuration file or through the environment.

> The same configuration variables can be used regardless of installation type
> (container or package-based).

### Variables

#### SL_APP_HOST

The `SL_APP_HOST` is the public-facing URL for the Stoplight application.

```
SL_APP_HOST="https://stoplight.example.com"
```

#### SL_API_HOST

The `SL_API_HOST` is the URL to the Stoplight API.

```
SL_API_HOST="https://stoplight-api.internal.example.com:3030"
```

#### SL_GITLAB_HOST

The `SL_GITLAB_HOST` is the full URL to the Stoplight GitLab instance

```
SL_GITLAB_HOST="https://gitlab.internal.example.com:8080"
```

#### SL_EXPORTER_HOST

The `SL_EXPORTER_HOST` is the full URL to the Stoplight GitLab instance:

```
SL_EXPORTER_HOST="https://stoplight-exporter.internal.example.com"
```

#### SL_PRISM_HOST

The `SL_PRISM_HOST` is the full URL to the Stoplight Prism instance

```
SL_PRISM_HOST="https://stoplight-prism.internal.example.com"
```

#### SL_PUBS_HOST

The `SL_PUBS_HOST` variable is the top-level domain used for documentation:

```
SL_PUBS_HOST="docs.example.com"
```

#### SL_PUBS_INGRESS

The `SL_PUBS_INGRESS` variable is the URL to the Stoplight Pubs instance admin API:

```
SL_PUBS_INGRESS="https://pubs.example.com:9098"
```

### RPM Package

The Stoplight App configuration is located at the location:

```bash
/etc/stoplight-app/stoplight-app.cfg
```

Be sure to customize any variables as needed to match your environment before
starting the API service.

> Any changes to the API configuration require a service restart in order to
> take effect.

### Docker

To expose configuration variables to the Docker runtime, either write them to a
file and use the `--env-file` argument:

```bash
cat <<EOF>app-env-vars
SL_API_HOST="..."
...
EOF

docker run --env-file app-env-vars ...
```

Or you can expose them one at a time with the `-e` flag:

```bash
docker run -e SL_API_HOST=https://stoplight-api.example.com ...
```

## Running

### RPM Package

To start the App server, run the command:

```bash
sudo systemctl start stoplight-app
```

Once started, you can see the status of the service using the command:

```bash
sudo systemctl status stoplight-app
```

### Docker

To start the App container, run the command:

```bash
docker run \
	--restart on-failure \
	--env-file app-env \
	-p 1234:3100 \
	quay.io/stoplight/app:latest
```

If started properly, the container should be marked with a healthy status after
30 seconds. Use the `docker ps` command to verify the container was started and
is running properly.

## Post-install Validations

Once the App component is running, you can verify the installation was
successful by visiting the app hostname and port in a web browser. If the web
page loads properly (what you see when visiting the [hosted
site](https://next.stoplight.io/login)), then you should be greeted with a login
screen, complete with images and styling.

If you would like to verify the app installation from the CLI, use `wget` to
search for any broken links:

```
wget -r -l2 –spider -D example.com http://example.com 2>&1 | grep -B1 'broken link!'
```

> Remember to replace 'example.com' above with the domain used to install the
> Stoplight application
