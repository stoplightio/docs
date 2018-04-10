# Stoplight Prism

The __Prism__ component powers scenarios and API orchestration.

> #### Networking Details
>
> The default port for the Prism component is TCP port __4050__ (HTTP). The port can be configured via configuration (see below).

## Installation

Prism can be installed with Docker or via RPM package.

### RPM Package

Prior to installing the RPM package, you will need to have the Stoplight package repository installed and configured with your user-specific credentials. 

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

Once the repository is configured properly, you can install the Pubs component using the command:

```bash
sudo yum install prism -y
```

### Docker Installation

To install the Pubs component with Docker, run the command below:

```bash
docker pull quay.io/stoplight/prism-multi
```

> Note, if you have not already authenticated with the Stoplight container registry, you will be prompted for credentials

## Configuring and Running

To configure the Prism component, you will need to provide runtime settings and connection details to the Stoplight App, API, and Exporter.

> Pubs uses the Stoplight API for authentication if using SSO within your published documentation, however it is not required

### Package-based Installations

#### Configuring the Service

The Prism configuration is located at `/etc/prism/prism.cfg`:

```bash
# URL to the Stoplight API
SL_API_HOST="http://localhost:3030"
# URL to the Stoplight App
SL_HOST="http://localhost:3100"
# URL to the Stoplight Exporter
SL_EXPORTER_HOST="http://localhost:3031"

# the following variables should be kept as the 
# default unless needed otherwise
ENV_NAME="production"
MAX_QUEUE_SIZE=500
MAX_RUNTIME_POOL_SIZE=15
MAX_WORKERS=25
PRISM_LOG_LEVEL="ERROR"
```

Be sure to customize any variable above as needed.

#### Starting the Service

To start the Prism server, run the command:

```bash
sudo systemctl start prism
```

Once started, you can see the status of the service using the command:

```bash
sudo systemctl status prism
```

### Docker Installations

#### Configuring the Container

The Prism container can be configured either via file (see the package configuration above) or via environment variables. If you would like to configure Prism via environment variable, use the variable names directly from the Prism configuration above.

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

#### Starting the Container

To start the Prism container, use the command:

```bash
docker run \
    --restart on-failure \
		--env-file prism-env-vars \
		-p 4050:4050 \
		quay.io/stoplight/prism-multi:latest
```

If started properly, the container should be marked with a healthy status after 30 seconds. Use the `docker ps` command to verify the container was started and is running properly.

## Post-install Validations

Once the Prism component is running, you can verify the installation was successful issuing an HTTP GET request to the `/health` URL on the HTTP admin port (set with `admin_bind`):

```bash
$ curl -v localhost:4050/health
Hello!
```

> Be sure to update the URL above to match your local installation

If Prism was installed and configured properly, you will receive an HTTP 200 response back.