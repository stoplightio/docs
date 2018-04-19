# Pubs (Hubs Server)

The **Pubs** component serves and catalogs Hubs published through Stoplight.

> #### Networking Details
>
> The default ports for the Pubs component are TCP ports **8080** (HTTP),
> **8443** (HTTPS), and **9098** (HTTPS optional). All ports can be customized.
>
> Pubs must be able to receive incoming connections from the following components:
>
> * User Clients (on the public-facing ports, which default to 8080 and 8443)
> * API (on the private admin port, which defaults to 9098)
> * Tasker (on the private admin port, which defaults to 9098)
>
> Pubs must be able to make outgoing connections to the following components:
>
> * API

> #### Component Dependencies
>
> Pubs has no component dependencies.

## Installation

Pubs can be installed with Docker or via RPM package.

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

> Make sure that the repository credentials are set before issuing the `cat` command above.

#### Installing the Pubs Package

Once the repository is configured properly, you can install the Pubs component
using the command:

```bash
sudo yum install pubs -y
```

### Docker Installation

To install the Pubs component with Docker, run the command below:

```bash
docker pull quay.io/stoplight/pubs
```

> Note, if you have not already authenticated with the Stoplight container
> registry, you will be prompted for credentials

## Configuration

To configure the Pubs component, you will need to provide connection details and
runtime settings.

### Variables

#### http_bind

The `http_bind` variable denotes the bind address/port to use when serving HTTP
traffic.

```yaml
http_bind: "127.0.0.1:8080"
```

#### https_bind

The `https_bind` variable denotes the bind address/port to use when serving
HTTPS traffic.

```yaml
https_bind: "127.0.0.1:8443"
```

#### ssl_enabled

The `ssl_enabled` variable denotes whether SSL should be enabled when serving
Hub requests.

```yaml
ssl_enabled: yes
```

> If `ssl_enabled` is set to `true`, then HTTP requests will automatically be
> redirected to HTTPS.

#### admin_bind

The `admin_bind` variable denotes the address/port to bind to when serving the
admin API.

```yaml
admin_bind: "127.0.0.1:9098"
```

#### admin_ssl_enabled

The `admin_ssl_enabled` variable denotes whether the admin API should accept
connections over HTTPS (as opposed to HTTP).

```yaml
admin_ssl_enabled: no
```

#### admin_ssl_cert_path

The `admin_ssl_cert_path` variable is the path to the SSL certificate to use
when serving TLS over the admin API.

```yaml
admin_ssl_cert_path: /path/to/cert
```

> This configuration option has no effect if `admin_ssl_enabled` is not set to
> `true`

#### admin_ssl_key_path

The `admin_ssl_key_path` variable is the path to the SSL key (matching the
`admin_ssl_cert_path` option) to use when serving TLS over the admin API.

```yaml
admin_ssl_key_path: /path/to/key
```

> This configuration option has no effect if `admin_ssl_enabled` is not set to
> `true`

#### admin_ip_whitelist

The `admin_ip_whitelist` variable is a list representing IP addresses that
should be allowed to connect to the admin API.

```yaml
admin_ip_whitelist:
  - 127.0.0.1
```

> If `admin_ip_whitelist` is not set, all IP addresses will be allowed to
> connect to the API.

#### data_dir

The `data_dir` variable is the directory to use when storing builds, build
metadata, and the pubs sqlite database.

```yaml
data_dir: /var/lib/pubs
```

#### static_ssl_domains

The `static_ssl_domains` variable can be used to serve static SSL certificates
for specific domain requests.

```yaml
static_ssl_domains:
  - domain: "*.example.com"
    cert-path: /path/to/example_com/certificate
    key-path: /path/to/example_com/key
```

> Include a leading star (`*`) in the domain if the certificate is wildcarded
> (ie, `*.example.com` for a wildcard certificate on the `example.com` domain).

### RPM Package

The Pubs default configuration is located at the path:

```bash
/etc/pubs/pubs.yml
```

Be sure to customize any variables as needed to match your environment before
starting the Pubs service.

> Any changes to the Pubs configuration require a service restart in order to
> take effect.

### Docker

The Pubs configuration can be mounted into a Docker container. As an example, if
a Pubs configuration file is located on the host system at the path:

```bash
/data/pubs.yml
```

This file can be mounted into the running Pubs container using the `-v` argument.

```bash
docker run -v /data/pubs.yml:/etc/pubs/pubs.yml ...
```

## Running

### RPM Package

To start the Pubs server, run the command:

```bash
sudo systemctl start pubs
```

Once started, you can see the status of the service using the command:

```bash
sudo systemctl status pubs
```

### Docker Installations

To start the Pubs container, use the command:

```bash
docker run \
	--restart on-failure \
	-v /path/to/pubs.yml:/etc/pubs/pubs.yml \
	-p 80:8080 \
	-p 443:8443 \
	-p 9098:9098 \
	quay.io/stoplight/pubs:latest
```

If started properly, the container should be marked with a healthy status after
30 seconds. Use the `docker ps` command to verify the container was started and
is running properly.

## Post-install Validations

Once the Pubs service is running, you can verify the installation was successful
issuing an `HTTP GET` request to the `/health` URL on the HTTP admin port (set
with `admin_bind`):

```bash
curl -v http://localhost:9098/health
```

> Be sure to update the URL above to match your local installation

If Pubs was installed and configured properly, you will receive an `HTTP 200`
response back.
