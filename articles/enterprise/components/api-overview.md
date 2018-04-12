# The Stoplight API

The **API** component powers the Stoplight backend, connecting the UI to the datastore and other miscellaneous Stoplight services.

> #### Networking Details
>
> The default port for the API component is TCP port **3030**. The port can be customized using the `PORT` environment variable.
>
> Make sure that the GitLab component is available **before** starting the API service.

## Installation

The Stoplight API can be installed with Docker or via RPM package.

> Before starting, be sure to complete the GitLab installation.

### RPM Package

Prior to installing the RPM package, you will need to:

* Install NodeJS

* Have the Stoplight package repository installed and configured with your user-specific credentials

#### Installing NodeJS

To install NodeJS, please run the following commands:

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

If you do not see a version starting `v8.9`, please contact Stoplight support for assistance.

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

#### Installing the API Package

Once the repository is configured properly, you can install the API component using the command:

```bash
sudo yum install stoplight-api -y
```

### Docker Installation

To install the API component with Docker, run the command below:

```bash
docker pull quay.io/stoplight/api
```

> Note, if the system you are using has not already authenticated with the
> Stoplight container registry, you will be prompted for credentials

## Configuring and Running

To configure the Stoplight API component, you will need to provide connection details to the other necessary Stoplight components.

### Package-based Installations

#### Configuring the Service

The Stoplight API configuration is located at the location:

```bash
/etc/stoplight-api/stoplight-api.cfg
```

The above file should contain the following entries:

```bash
# Secret used to encrypt cookies and other secrets used by the Stoplight API.
SIGN_SECRET="CHANGE_ME_TO_SOMETHING_RANDOM"

# Full URL to the GitLab postgres instance.
POSTGRES_URL="postgres://username:password@example.com:5432"

# Domain that Stoplight is being served from. For example, if
# Stoplight is being served from 'stoplight.example.com', set
# this to 'example.com'.
SL_COOKIE_DOMAIN="example.com"

# SL_APP_HOST is the full URL to the Stoplight app component.
SL_APP_HOST="http://localhost:3030"

# SL_API_HOST is the full URL to this (the Stoplight API) component.
SL_API_HOST="http://localhost:3030"

# SL_EXPORTER_HOST is the full URL to the Stoplight exporter component.
SL_EXPORTER_HOST="http://localhost:3031"

# SL_GITLAB_HOST is the full URL to the Stoplight GitLab instances HTTP port.
SL_GITLAB_HOST="http://localhost:8080"

# SL_REDIS_URL is the full URL to a Redis instance.
SL_REDIS_URL="redis://:password@exampl.com:6379"
```

> Please note that the `SIGN_SECRET` environment variable must remain static between service restarts

Be sure to customize any of the variables above as needed.

#### Starting the Service

To start the API server, run the command:

```bash
sudo systemctl start stoplight-api
```

Once started, you can see the status of the service using the command:

```bash
sudo systemctl status stoplight-api
```

### Docker Installations

#### Configuring the Container

The Stoplight API container requires the following environment variables be exposed to the running instance:

```bash
# Secret used to encrypt cookies and other secrets used by the Stoplight API.
SIGN_SECRET="CHANGE_ME_TO_SOMETHING_RANDOM"

# Full URL to the GitLab postgres instance.
POSTGRES_URL="postgres://username:password@example.com:5432"

# Domain that Stoplight is being served from. For example, if
# Stoplight is being served from 'stoplight.example.com', set
# this to 'example.com'.
SL_COOKIE_DOMAIN="example.com"

# SL_APP_HOST is the full URL to the Stoplight app component.
SL_APP_HOST="http://localhost:3030"

# SL_API_HOST is the full URL to this (the Stoplight API) component.
SL_API_HOST="http://localhost:3030"

# SL_EXPORTER_HOST is the full URL to the Stoplight exporter component.
SL_EXPORTER_HOST="http://localhost:3031"

# SL_GITLAB_HOST is the full URL to the Stoplight GitLab instances HTTP port.
SL_GITLAB_HOST="http://localhost:8080"

# SL_REDIS_URL is the full URL to a Redis instance.
SL_REDIS_URL="redis://:password@exampl.com:6379"
```

> Please note that the `SIGN_SECRET` environment variable must remain static between service restarts

To expose these to the Docker runtime, either write them to a file and use the `--env-file` argument:

```bash
cat <<EOF>api-env-vars
SL_APP_HOST="..."
...
EOF

docker run --env-file api-env-vars ...
```

Alternatively, you can expose them one at a time with the `-e` flag:

```bash
docker run -e SL_APP_HOST=https://stoplight.example.com ...
```

#### Starting the Container

To start the API container, run the command:

```bash
docker run \
        --restart on-failure \
		--env-file api-env \
		-p 2345:3030 \
		quay.io/stoplight/api:latest
```

If started properly, the container should be marked with a healthy status after 30 seconds. Use the `docker ps` command to verify the container was started and is running properly.

## Post-install Validations

Once the API component is running, you can verify the installation was successful issuing an HTTP GET request to the `/health` endpoint:

```bash
# be sure to update the port here to match the installation port
curl -v http://localhost:3030/health
```

If the API was installed and configured properly, you will receive an HTTP 200 response back.
