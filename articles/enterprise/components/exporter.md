# The Stoplight Exporter

The **Exporter** component de-references JSON specifications to ensure all
referenced files and external data sources are resolved when needed.

> #### Networking Details
>
> The default port for the Exporter component is TCP port **3031**. The port can
> be customized using the `PORT` configuration variable.
>
> The Exporter must be able to receive incoming connections from the following components:
>
> * User Clients (web browser or desktop application)
> * App
> * API
> * Prism
>
> The Exporter must be able to make outgoing connections to the following components:
>
> * API

> #### Component Dependencies
>
> The Exporter is stateless, and has no component dependencies.

## Installation

The Stoplight Exporter can be installed with Docker or via RPM package.

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

> Make sure that the repository credentials are set before issuing the `cat` command above.

#### Installing the Exporter Package

Once the repository is configured properly, you can install the Exporter component using the command:

```bash
sudo yum install stoplight-exporter -y
```

### Docker

To install the Exporter component with Docker, run the command below:

```bash
docker pull quay.io/stoplight/exporter
```

> Note, if you have not already authenticated with the Stoplight container
> registry, you will be prompted for credentials

## Configuration

To configure the Stoplight Exporter component, you will need to provide runtime
values and connection details to the other necessary Stoplight components. The
Exporter can be configured either by the configuration file or through the
environment.

> The same configuration variables can be used regardless of installation type
> (container or package-based).

### Variables

#### SL_APP_HOST

The `SL_APP_HOST` is the public-facing URL for the Stoplight App.

```
SL_APP_HOST="https://stoplight.example.com"
```

#### SL_API_HOST

The `SL_API_HOST` variable is the URL to the Stoplight API.

```
SL_API_HOST="https://stoplight-api.internal.example.com:3030"
```

#### SL_EXPORTER_HOST

The `SL_EXPORTER_HOST` variable is the full URL to the Stoplight Exporter instance.

```
SL_EXPORTER_HOST="https://stoplight-exporter.internal.example.com"
```

### RPM Package

The Stoplight Exporter configuration is located at the location:

```bash
/etc/stoplight-exporter/stoplight-exporter.cfg
```

Be sure to customize any variables as needed to match your environment
**before** starting the Exporter service.

> Any changes to the Exporter configuration requires a service restart in order
> to take effect.

### Docker

To expose these to the Docker runtime, either write them to a file and use the `--env-file` argument:

```bash
cat <<EOF>exporter-env-vars
SL_APP_HOST="..."
...
EOF

docker run --env-file exporter-env-vars ...
```

Alternatively, you can expose them one at a time with the `-e` flag:

```bash
docker run -e SL_APP_HOST=https://stoplight.example.com ...
```

## Running

### RPM Package

To start the Exporter server, run the command:

```bash
sudo systemctl start stoplight-exporter
```

Once started, you can see the status of the service using the command:

```bash
sudo systemctl status stoplight-exporter
```

### Docker

To start the Exporter container, run the command:

```bash
docker run \
	--restart on-failure \
	--env-file exporter-env \
	-p 2345:3031 \
	quay.io/stoplight/exporter:latest
```

If started properly, the container should be marked with a healthy status after
30 seconds. Use the `docker ps` command to verify the container was started and
is running properly.

## Post-install Validations

Once the Exporter component is running, you can verify the installation was
successful issuing an `HTTP GET` request to the root (`/`) endpoint:

```bash
# be sure to update the scheme, host, and port to match the installation port
curl -v http://localhost:3031/
```

If the Exporter was installed and configured properly, you will receive an `HTTP 200` reponse back.
