# Prism

The **Prism** component powers scenarios and API orchestration.

> #### Networking Details
>
> The default port for the Prism component is TCP port **4050** (HTTP). The port can be configured via configuration (see below).
>
> Prism must be able to receive incoming connections from the following components:
>
> * User Clients (web browser or desktop application)
> * App
> * API
>
> Prism must be able to make outgoing connections to the following components:
>
> * Exporter

> #### Component Dependencies
>
> Make sure the following components are available **before** starting the API
> service:
>
> * PostgreSQL
> * Redis
> * Gitlab

## Installation

Prism can be installed with Docker or via RPM package.

### RPM Package

Prior to installing the RPM package, you will need to have the Stoplight package
repository installed and configured with your user-specific credentials.

#### Setting up the Package Repository

You can setup the Stoplight package repo by copying-and-pasting the contents
below into a terminal:

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

#### Installing the Prism Package

Once the repository is configured properly, you can install the Pubs component using the command:

```bash
sudo yum install prism -y
```

### Docker

To install the Pubs component with Docker, run the command below:

```bash
docker pull quay.io/stoplight/prism-multi
```

> Note, if you have not already authenticated with the Stoplight container
> registry, you will be prompted for credentials.

## Configuration

To configure the Prism component, you will need to provide runtime settings and
connection details to the Stoplight App, API, and Exporter.

### Variables

#### SL_API_HOST

The `SL_API_HOST` variable is the full URL to the Stoplight API.

```
SL_API_HOST="http://localhost:3030"
```

#### SL_HOST

The `SL_HOST` variable is the full URL to the Stoplight App.

```
SL_HOST="http://localhost:3100"
```

#### SL_EXPORTER_HOST

The `SL_EXPORTER_HOST` variable is the URL to the Stoplight Exporter.

```
SL_EXPORTER_HOST="http://localhost:3031"
```

#### ENV_NAME

The `ENV_NAME` variable is a flag noting the environment level.

```
ENV_NAME="production"
```

> `ENV_NAME` should be left as `production` unless instructed otherwise by the
> Stoplight Support staff.

#### MAX_QUEUE_SIZE

The `MAX_QUEUE_SIZE` variable denotes the internal queue size used to service
requests.

```
MAX_QUEUE_SIZE=500
```

> `MAX_QUEUE_SIZE` should be left as `500` unless instructed otherwise by the
> Stoplight Support staff.

#### MAX_RUNTIME_POOL_SIZE

The `MAX_RUNTIME_POOL_SIZE` variable denotes the worker pool size used to
service requests.

```
MAX_RUNTIME_POOL_SIZE=15
```

> `MAX_RUNTIME_POOL_SIZE` should be left as `15` unless instructed otherwise by
> the Stoplight Support staff.

#### MAX_WORKERS

The `MAX_WORKERS` variable denotes the number of worker threads to use when
servicing requests.

```
MAX_WORKERS=25
```

> `MAX_WORKERS` should be left as `25` unless instructed otherwise by the
> Stoplight Support staff.

#### PRISM_LOG_LEVEL

The `PRISM_LOG_LEVEL` variable denotes the log level of the Prism process.

```
PRISM_LOG_LEVEL="ERROR"
```

> `PRISM_LOG_LEVEL` should be left as `ERROR` unless instructed otherwise by the
> Stoplight Support staff.

### RPM Package

The Prism configuration file is located at the location:

```bash
/etc/prism/prism.cfg
```

Be sure to customize any variables as needed to match your environment before
starting the Prism service.

> Any changes to the Prism configuration require a service restart in order to
> take effect.

### Docker

The Prism container can be configured either via file (see the package
configuration above) or via environment variables. If you would like to
configure Prism via environment variable, use the variable names directly from
the Prism configuration above.

To expose variables to the Docker runtime, either write them to a file and use the `--env-file` argument:

```bash
cat <<EOF>prism-env-vars
SL_API_HOST="..."
...
EOF

docker run --env-file prism-env-vars ...
```

Alternatively, you can expose them one at a time with the `-e` flag:

```bash
docker run -e SL_API_HOST=api.stoplight.example.com ...
```

## Running

### RPM Package

To start the Prism server, run the command:

```bash
sudo systemctl start prism
```

Once started, you can see the status of the service using the command:

```bash
sudo systemctl status prism
```

### Docker

To start the Prism container, use the command:

```bash
docker run \
	--restart on-failure \
	--env-file prism-env-vars \
	-p 4050:4050 \
	quay.io/stoplight/prism-multi:latest
```

If started properly, the container should be marked with a healthy status after
30 seconds. Use the `docker ps` command to verify the container was started and
is running properly.

## Post-install Validations

Once the Prism component is running, you can verify the installation was
successful issuing an HTTP GET request to the `/health` URL on the HTTP admin
port (set with `admin_bind`):

```bash
$ curl -v localhost:4050/health
Hello!
```

> Be sure to update the URL above to match your local installation

If Prism was installed and configured properly, you will receive an `HTTP 200`
response back.
