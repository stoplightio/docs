# Stoplight Tasker

The __Tasker__ component runs scheduled and on-demand tasks for the Stoplight platform.

> #### Networking Details
>
> The default port for the Tasker component is TCP port __9432__. 
> 
> The port and bind address can be configured via the `TASKER_HTTP_BIND` environment variable or the `--listen` CLI flag.
> 
> Tasker requires a Redis instance to be available when starting. Be sure to setup Redis before installing Tasker.

## Installation

Tasker can be installed with Docker or via RPM package.

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

Once the repository is configured properly, you can install the Tasker component using the command:

```bash
sudo yum install tasker -y
```

### Docker Installation

To install the Tasker component with Docker, run the command below:

```bash
docker pull quay.io/stoplight/tasker
```

> Note, if you have not already authenticated with the Stoplight container registry, you will be prompted for credentials

## Configuring and Running

To configure the Tasker component, you will need to provide runtime settings and connection details for a running Redis instance.

### Package-based Installations

#### Configuring the Service

The Tasker configuration is located at:

```bash
/etc/tasker/tasker.cfg
```

The above file should contain the following entries:

```bash
# Tasker HTTP bind address (host:port)
TASKER_HTTP_BIND="localhost:9432"

# Tasker execution mode, either 'shell' or 'docker'
TASKER_MODE="shell"
# If using 'shell' mode, provide path to stoplight-hub-builder package root
CORE_ROOT="/opt/stoplight-hub-builder"

# Redis host:port to connect to (must be available before starting service)
TASKER_REDIS_HOSTPORT="redis:6379"
# Redis password, if any
TASKER_REDIS_PASSWORD=""
# Redis database
TASKER_REDIS_DATABASE="0"
# Redis namespace
TASKER_REDIS_NAMESPACE=""
```

Be sure to customize any variable above as needed.

#### Starting the Service

To start the Tasker server, run the command:

```bash
sudo systemctl start tasker
```

Once started, you can see the status of the service using the command:

```bash
sudo systemctl status tasker
```

### Docker Installations

#### Configuring the Container

The Tasker container can be configured via the following environment variables:

```bash
# Tasker HTTP bind address (host:port)
TASKER_HTTP_BIND="localhost:9432"

# Tasker execution mode, either 'shell' or 'docker'
TASKER_MODE="shell"
# If using 'shell' mode, provide path to stoplight-hub-builder package root
CORE_ROOT="/opt/stoplight-hub-builder"

# Redis host:port to connect to (must be available before starting service)
TASKER_REDIS_HOSTPORT="redis:6379"
# Redis password, if any
TASKER_REDIS_PASSWORD=""
# Redis database
TASKER_REDIS_DATABASE="0"
# Redis namespace
TASKER_REDIS_NAMESPACE=""
```

To expose these to the Docker runtime, either write them to a file and use the `--env-file` argument:

```bash
cat <<EOF>tasker-env-vars
TASKER_HTTP_BIND="..."
...
EOF

docker run --env-file tasker-env-vars ...
```

Alternatively, you can expose them one at a time with the `-e` flag:

```bash
docker run -e TASKER_HTTP_BIND=0.0.0.0:9432 ...
```

#### Starting the Container

To start the Tasker container, use the command:

```bash
docker run \
    --restart on-failure \
		--env-file tasker-env-vars \
		-p 9432:9432 \
		quay.io/stoplight/tasker:latest
```

If started properly, the container should be marked with a healthy status after 30 seconds. Use the `docker ps` command to verify the container was started and is running properly.

## Post-install Validations

Once the Tasker component is running, you can verify the installation was successful issuing an HTTP GET request to the `/health` endpoint:

```bash
# be sure to update the port here to match the installation port
curl -v http://localhost:9432/health
```

If Tasker was installed and configured properly, you will receive an HTTP 200 reponse back.