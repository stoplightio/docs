# Stoplight Pubs

The __Pubs__ component serves and catalogs hubs published through Stoplight.

> #### Networking Details
>
> The default ports for the Pubs component are TCP ports __8080__ (HTTP), __8443__ (HTTPS), and __9098__ (HTTPS optional). All ports can be configured via configuration (see below).

## Installation

Pubs can be installed with Docker or via RPM package.

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
sudo yum install pubs -y
```

### Docker Installation

To install the Pubs component with Docker, run the command below:

```bash
docker pull quay.io/stoplight/pubs
```

> Note, if you have not already authenticated with the Stoplight container registry, you will be prompted for credentials

## Configuring and Running

To configure the Pubs component, you will need to provide runtime settings and connection details to the Stoplight Pubs.

> Pubs uses the Stoplight API for authentication if using SSO within your published documentation, however it is not required

### Package-based Installations

#### Configuring the Service

The Pubs configuration is located at:

```bash
/etc/pubs/pubs.yml
```

The above file should contain the following entries:

```bash
# Bind address/port to serve HTTP traffic on
http_bind: "127.0.0.1:8080"

# Bind address/port to serve HTTPS traffic on, if enabled (see below)
https_bind: "127.0.0.1:8443"

# Whether to enable SSL, powered by LetsEncrypt. If true, HTTP serving is
# disabled.
ssl_enabled: yes

# Bind address/port to server admin/management API
admin_bind: "127.0.0.1:9098"

# Whether to enable SSL when serving admin API
admin_ssl_enabled: no
# If SSL is enabled for the management API, a certificate and key must be
# provided
admin_ssl_cert_path: 
admin_ssl_key_path: 

# If set, only requests with the following IPs will be responded to by the admin
# API
admin_ip_whitelist:
  # - 127.0.0.1

# Directory to store builds, build metadata, and dynamically-generated
# certificates
data_dir: /var/lib/pubs
```

Be sure to customize any variable above as needed.

#### Starting the Service

To start the Pubs server, run the command:

```bash
sudo systemctl start pubs
```

Once started, you can see the status of the service using the command:

```bash
sudo systemctl status pubs
```

### Docker Installations

#### Configuring the Container

The Pubs container can be configured either via file (see the package configuration above) or via environment variables. If you would like to configure Pubs via environment variable, use the variable naming conventions from the configuration file above and prepend a `PUBS_` prefix to them.

For example, to set the HTTP bind address through the environment, use the variable:

```
PUBS_HTTP_BIND="localhost:8080"
```

> Be sure to capitalize all letters and prefix environment variables with `PUBS_` (ie, `ssl_enabled` becomes `PUBS_SSL_ENABLED`)

To expose these to the Docker runtime, either write them to a file and use the `--env-file` argument:

```bash
cat <<EOF>pubs-env-vars
PUBS_HTTP_BIND="..."
...
EOF

docker run --env-file pubs-env-vars ...
```

Alternatively, you can expose them one at a time with the `-e` flag:

```bash
docker run -e PUBS_HTTP_BIND=0.0.0.0:80 ...
```

#### Starting the Container

To start the Pubs container, use the command:

```bash
docker run \
    --restart on-failure \
		--env-file pubs-env-vars \
		-p 80:8080 \
		-p 443:8443 \
		-p 9098:9098 \
		quay.io/stoplight/pubs:latest
```

If started properly, the container should be marked with a healthy status after 30 seconds. Use the `docker ps` command to verify the container was started and is running properly.

## Post-install Validations

Once the Pubs component is running, you can verify the installation was successful issuing an HTTP GET request to the `/health` URL on the HTTP admin port (set with `admin_bind`):

```bash
curl -v http://localhost:9098/health
```

> Be sure to update the URL above to match your local installation

If Pubs was installed and configured properly, you will receive an HTTP 200 response back.