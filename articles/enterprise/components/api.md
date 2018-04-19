# The Stoplight API

The **API** component powers the Stoplight backend, connecting the UI to the
datastore and other miscellaneous Stoplight services.

> #### Networking Details
>
> The default port for the API component is TCP port **3030**. The port can be
> customized using the `PORT` configuration variable.
>
> The API must be able to receive incoming connections from the following components:
>
> * User Clients (web browser or desktop application)
> * App
>
> The API must be able to make outgoing connections to the following components:
>
> * PostgreSQL
> * Redis
> * Gitlab
> * Exporter
> * Prism

> #### Component Dependencies
>
> Make sure the following components are available **before** starting the API
> service:
>
> * PostgreSQL
> * Redis
> * Gitlab

## Installation

The Stoplight API can be installed with Docker or RPM package.

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

> Make sure that the repository credentials are set before issuing the `cat` command above.

#### Installing the API Package

Once the repository is configured properly, you can install the API component
using the command:

```bash
sudo yum install stoplight-api -y
```

### Docker

To install the API component with Docker, run the command below:

```bash
docker pull quay.io/stoplight/api
```

> Note, if the system you are using has not already authenticated with the
> Stoplight container registry, you will be prompted for credentials.

## Configuration

To configure the Stoplight API component, you will need to provide runtime
values and connection details to the other necessary Stoplight components. The
API can be configured either by the configuration file or through the
environment.

> The same configuration variables can be used regardless of installation type
> (container or package-based).

### Variables

#### SIGN_SECRET

The `SIGN_SECRET` variable is used to encrypt session cookies and other secrets
used by the Stoplight API.

```
SIGN_SECRET="CHANGE_ME_TO_SOMETHING_RANDOM"
```

There is no minimum or maximum character requirement, however Stoplight
recommends using a random string more than 32 characters in length for
production environments.

> Note that the `SIGN_SECRET` configuration variable must remain static between
> service restarts

#### POSTGRES_URL

The `POSTGRES_URL` variable is the connection URI for the PostgreSQL database
shared with Gitlab.

```
POSTGRES_URL="postgres://username:password@example.com:5432/database_name"
```

#### SL_COOKIE_DOMAIN

The `SL_COOKIE_DOMAIN` variable is the name of the top-level domain that
Stoplight is being served from.

```
SL_COOKIE_DOMAIN="example.com"
```

For example, if Stoplight is being served from the `stoplight.example.com`
domain, set this variable to `example.com`.

#### SL_APP_HOST

The `SL_APP_HOST` variable is the full URL to the Stoplight app component.

```
SL_APP_HOST="http://localhost:3030"
```

#### SL_API_HOST

The `SL_API_HOST` variable is the full URL to this (the Stoplight API) component.

```
SL_API_HOST="http://localhost:3030"
```

#### SL_EXPORTER_HOST

The `SL_EXPORTER_HOST` variable is the full URL to the Stoplight exporter component.

```
SL_EXPORTER_HOST="http://localhost:3031"
```

#### SL_GITLAB_HOST

The `SL_GITLAB_HOST` variable is the full URL to the Stoplight GitLab instances HTTP port.

```
SL_GITLAB_HOST="http://localhost:8080"
```

#### SL_REDIS_URL

The `SL_REDIS_URL` variable is the full URL to a Redis instance.

```
SL_REDIS_URL="redis://:password@example.com:6379"
```

#### DISABLE_REGISTRATION

The `DISABLE_REGISTRATION` variable can be used to prevent new users from
registering with Stoplight. Enabling this feature does not prevent existing
users from inviting new users.

```
DISABLE_REGISTRATION=false
```

If this option is set to `true`, new user registration requests will receive the
following error when attempting to register:

> User registration has been temporarily disabled. Please contact your administrator.

### RPM Package

The Stoplight API configuration file is located at the path:

```bash
/etc/stoplight-api/stoplight-api.cfg
```

Be sure to customize any variables as needed to match your environment before
starting the API service.

> Any changes to the API configuration requires a service restart in order to
> take effect.

### Docker

To expose configuration variables to the Docker runtime, either write them to a
file and use the `--env-file` argument:

```bash
cat <<EOF>api-env-vars
SL_APP_HOST="..."
...
EOF

docker run --env-file api-env-vars ...
```

Or you can expose them one at a time with the `-e` flag:

```bash
docker run -e SL_APP_HOST=https://stoplight.example.com ...
```

## Running

### RPM Package

To start the API server, run the command:

```bash
sudo systemctl start stoplight-api
```

Once started, you can see the status of the service using the command:

```bash
sudo systemctl status stoplight-api
```

### Docker

To start the API container, run the command:

```bash
docker run \
	--restart on-failure \
	-p 3030:3030 \
	quay.io/stoplight/api:latest
```

> Remember to set any necessary environment variables

If started properly, the container should be marked with a healthy status after
30 seconds. Use the `docker ps` command to verify the container was started and
is running properly.

## Post-install Validations

Once the API component is running, you can verify the installation was
successful issuing an `HTTP GET` request to the `/health` endpoint:

```bash
# remember to update the scheme, host, and port here to match your installation
curl -v http://localhost:3030/health
```

If the API was installed and configured properly, you will receive an `HTTP 200`
response back.
