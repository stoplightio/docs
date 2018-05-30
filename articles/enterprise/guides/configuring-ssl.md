# Configuring SSL

This guide covers how to protect network communication for the Stoplight
platform using SSL.

## Prerequisites

In order to configure the Stoplight platform to use SSL, you will need:

* A method for generating (one or many) SSL private keys and certificates for
  each component.
* A method for having the certificates above signed by a trusted [Certificate
  Authority](https://en.wikipedia.org/wiki/Certificate_authority) (or CA),
  either internal or external to your organization.
* If you are using self-signed certificates or certificates signed by an
  internal CA, you will need a method for establishing trust on the component
  and client systems.

> Please note, this guide _does not_ cover the details of creating, signing, or
> establishing trust of certificates on component or client systems. If you are
> unsure of how to perform any of the prerequisite items, please consult with
> your internal IT team.

## Components

The method for configuring SSL varies by component. Please see the component
sections below to get started.

### App, API, Exporter, Prism, Tasker

In order to configure SSL for the **App**, **API**, **Exporter**, **Prism**, and
**Tasker** components, you must use a [reverse
proxy](https://en.wikipedia.org/wiki/Reverse_proxy) for HTTPS/SSL termination.
This means that the component itself will not communicate over SSL, but a proxy
sitting in front of the component will. For more information on SSL termination,
please see [here](https://en.wikipedia.org/wiki/TLS_termination_proxy).

If you do not already have a reverse proxy application chosen, Stoplight uses
and recommends [NGINX](http://nginx.org/). See the section below for an example
configuration.

#### Configuring NGINX

To configure NGINX to use SSL, Stoplight recommends using the following
configuration:

```nginx
server {
    # optional, but required if serving multiple components from same proxy
    server_name component.example.com;
    server_tokens off;

    listen 443 ssl http2 default_server;

    ssl on;
    # customize pased on local filesystem
    ssl_certificate     /path/to/ssl/cert;
    ssl_certificate_key /path/to/ssl/key;

    ssl_session_cache         shared:SSL:20m;
    ssl_session_timeout       60m;
    ssl_protocols             TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    ssl_ciphers               ECDH+AESGCM:ECDH+AES256:ECDH+AES128:DH+3DES:!ADH:!AECDH:!MD5;
    add_header                Strict-Transport-Security "max-age=31536000; includeSubDomains" always;

    location / {
        # customize the port and IP per component being served
        proxy_pass http://127.0.0.1:PORT;

        client_max_body_size 0;
        gzip off;
        proxy_http_version 1.1;
        proxy_read_timeout 300;
        proxy_connect_timeout 300;
        proxy_redirect off;

        proxy_set_header    Upgrade $http_upgrade;
        proxy_set_header    Connection "upgrade";
        proxy_set_header    Host                $http_host;
        proxy_set_header    X-Real-IP           $remote_addr;
        proxy_set_header    X-Forwarded-Ssl     on;
        proxy_set_header    X-Forwarded-For     $proxy_add_x_forwarded_for;
        proxy_set_header    X-Forwarded-Proto   $scheme;
        proxy_set_header    X-Frame-Options     SAMEORIGIN;
    }

}
```

To automatically redirect HTTP to HTTPS, add the following section to the nginx
configuration:

```nginx
server {
    # optional, but required if serving multiple components from same proxy
    server_name              component.example.com;
    server_tokens off;

    listen                   80;
    listen                   [::]:80;

    return                   301 https://$server_name$request_uri;
}
```

### Pubs

To configure the Pubs component to use HTTPS, update the configuration with
following entries:

```yaml
# Whether to enable SSL when serving admin API (protecting communication
# between the API and Pubs)
admin_ssl_enabled: yes
admin_ssl_cert_path: "/path/to/ssl/cert"
admin_ssl_key_path: "/path/to/ssl/key"

# Whether to enable SSL when serving published docs
ssl_enabled: yes
https_bind: "0.0.0.0:443"
static_ssl_domains:
  # must match the any domains docs are published under. can specify many.
  - domain: "*.docs.example.com"
    cert-path: "/path/to/docs.example.com/certificate"
    key-path: "/path/to/docs.example.com/key"
```

> Remember to update the path elements above to match the filesystem path to the
> SSL keys and certificates

All SSL certificates must match the hostnames (ie, domain names) they are served
from.

### GitLab

Configuring GitLab to use SSL varies depending on the installation type. Please
see below for more information.

> If you are unsure of your installation type, please contact [Stoplight
> Support](mailto:support@stoplight.io) for assistance.

#### Omnibus Installations (default)

For Omnibus installations, please see the official GitLab documentation below:

* [Configuring the embedded NGINX process to use SSL](https://docs.gitlab.com/omnibus/settings/nginx.html)

* [General information on how GitLab SSL settings work](https://docs.gitlab.com/omnibus/settings/ssl.html)

#### From-Source Installations

For from-source installations, please see
[here](https://github.com/stoplightio/docker-gitlab#ssl).
