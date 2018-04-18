# Tasker (Jobs Server)

The **Tasker** component runs scheduled and on-demand tasks for the Stoplight platform.

> #### Networking Details
>
> The default port for the Tasker component is TCP port **9432**. This port can
> be customzied via configuration variable.
>
> Tasker must be able to receive incoming connections from the following components:
>
> * API
>
> Tasker must be able to make outgoing connections to the following components:
>
> * API
> * Redis
> * Pubs

> #### Component Dependencies
>
> Make sure the following components are available **before** starting the Tasker
> service:
>
> * Redis

## Installation

Tasker can be installed with Docker or via RPM package.

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

#### Installing the Tasker Package

Once the repository is configured properly, you can install the Tasker component using the command:

```bash
sudo yum install tasker -y
```

### Docker

To install the Tasker component with Docker, run the command below:

```bash
docker pull quay.io/stoplight/tasker
```

> Note, if you have not already authenticated with the Stoplight container
> registry, you will be prompted for credentials.

## Configuration

To configure the Tasker component, you will need to provide runtime settings and
connection details for a running Redis instance.

### Variables

#### TASKER_HTTP_BIND

The `TASKER_HTTP_BIND` variable is the bind address and port used for serving
the Tasker HTTP API.

```
TASKER_HTTP_BIND="localhost:9432"
```

#### TASKER_MODE

The `TASKER_MODE` variable is the operation mode that Tasker should use when
executing jobs. Valid values for `TASKER_MODE` are `docker` and `shell`.

```
TASKER_MODE="shell"
```

> If not specified, Tasker defaults to using `docker` mode.

#### CORE_ROOT

The `CORE_ROOT` denotes the absolutel path to stoplight-hub-builder package root.

```
CORE_ROOT="/opt/stoplight-hub-builder"
```

> This variable is only required when running in `shell` mode.

#### TASKER_REDIS_HOSTPORT

The `TASKER_REDIS_HOSTPORT` variable denotes the Redis instance host:port to connect to.

```
TASKER_REDIS_HOSTPORT="redis://redis:6379"
```

> Redis must be available before starting service.

#### TASKER_REDIS_PASSWORD

The `TASKER_REDIS_PASSWORD` variable is an optional password to use when
connecting to the Redis instance.

```
TASKER_REDIS_PASSWORD=""
```

#### TASKER_REDIS_DATABASE

The `TASKER_REDIS_DATABASE` variable is the Redis database used by Tasker for
storing job state.

```
TASKER_REDIS_DATABASE="0"
```

#### TASKER_REDIS_NAMESPACE

The `TASKER_REDIS_NAMESPACE` variable is the Redis namespace used by Tasker for
storing job state.

```
TASKER_REDIS_NAMESPACE="tasker"
```

### RPM Package

The Tasker configuration is located at:

```bash
/etc/tasker/tasker.cfg
```

Be sure to customize any variables as needed to match your environment before
starting the Tasker service.

> Any changes to the Tasker configuration require a service restart in order to
> take effect.

### Docker

To expose these to the Docker runtime, either write them to a file and use the
`--env-file` argument:

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

## Running

### RPM Package

To start the Tasker server, run the command:

```bash
sudo systemctl start tasker
```

Once started, you can see the status of the service using the command:

```bash
sudo systemctl status tasker
```

### Docker

To start the Tasker container, use the command:

```bash
docker run \
	--restart on-failure \
	--env-file tasker-env-vars \
	-p 9432:9432 \
	quay.io/stoplight/tasker:latest
```

If started properly, the container should be marked with a healthy status after
30 seconds. Use the `docker ps` command to verify the container was started and
is running properly.

## Post-install Validations

Once the Tasker component is running, you can verify the installation was
successful issuing an `HTTP GET` request to the `/health` endpoint:

```bash
# remember to update the scheme, host, and port here to match your installation
curl -v http://localhost:9432/health
```

If Tasker was installed and configured properly, you will receive an `HTTP 200`
reponse back.
