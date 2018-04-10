# The Stoplight Exporter

The __Exporter__ component de-references JSON specifications to ensure all referenced files and external data sources are resolved when needed.

> #### Networking Details
>
> The default port for the API component is TCP port __3031__. The port can be customized using the `PORT` environment variable.
> 
> The Exporter service is stateless and relies on no other components for operation.

## Installation

The Stoplight Exporter can be installed with Docker or via RPM package.

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

#### Installing the Exporter Package

Once the repository is configured properly, you can install the Exporter component using the command:

```bash
sudo yum install stoplight-exporter -y
```

### Docker Installation

To install the API component with Docker, run the command below:

```bash
docker pull quay.io/stoplight/exporter
```

> Note, if you have not already authenticated with the Stoplight container registry, you will be prompted for credentials

## Configuring and Running

To configure the Stoplight Exporter component, you will need to provide connection details to the other necessary Stoplight components.

### Package-based Installations

#### Configuring the Service

The Stoplight API configuration is located at the location:

```bash
/etc/stoplight-exporter/stoplight-exporter.cfg
```

The above file should contain the following entries:

```bash
# SL_APP_HOST is the public-facing URL for the stoplight application
SL_APP_HOST="https://stoplight.example.com"

# SL_API_HOST is the URL to the Stoplight API
SL_API_HOST="https://stoplight-api.internal.example.com:3030"

# SL_EXPORTER_HOST is the full URL to the Stoplight Gitlab instance
SL_EXPORTER_HOST="https://stoplight-exporter.internal.example.com"

# SL_PREVIEW_HOST is the full URL to the Stoplight Preview instance
SL_PREVIEW_HOST="https://stoplight-preview.internal.example.com"
```

Be sure to customize any variable above as needed.

#### Starting the Service

To start the API server, run the command:

```bash
sudo systemctl start stoplight-exporter
```

Once started, you can see the status of the service using the command:

```bash
sudo systemctl status stoplight-exporter
```

### Docker Installations

#### Configuring the Container

The Stoplight Exporter container requires the following environment variables be exposed to the running instance:

```bash
# SL_APP_HOST is the public-facing URL for the stoplight application
SL_APP_HOST="https://stoplight.example.com"

# SL_API_HOST is the URL to the Stoplight API
SL_API_HOST="https://stoplight-api.internal.example.com:3030"

# SL_EXPORTER_HOST is the full URL to the Stoplight Gitlab instance
SL_EXPORTER_HOST="https://stoplight-exporter.internal.example.com"

# SL_PREVIEW_HOST is the full URL to the Stoplight Preview instance
SL_PREVIEW_HOST="https://stoplight-preview.internal.example.com"
```

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

#### Starting the Container

To start the API container, run the command:

```bash
docker run \
    --restart on-failure \
		--env-file exporter-env \
		-p 2345:3031 \
		quay.io/stoplight/exporter:latest
```

If started properly, the container should be marked with a healthy status after 30 seconds. Use the `docker ps` command to verify the container was started and is running properly.

## Post-install Validations

Once the Exporter component is running, you can verify the installation was successful issuing an HTTP GET request to the root (`/`) endpoint:

```bash
# be sure to update the port here to match the installation port
curl -v http://localhost:3031/
```

If the Exporter was installed and configured properly, you will receive an HTTP 200 reponse back.