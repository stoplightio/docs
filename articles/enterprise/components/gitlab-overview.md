# Gitlab CE

Gitlab CE powers the Stoplight backend, including file storage and database.

> ### Requirements
> 
> #### Storage
> 
> Gitlab requires persistent storage in order to store Stoplight file data (in git), and optionally PostgreSQL data (when using the omnibus package).
> 
> #### Networking
>
> The default port for Gitlab's HTTP API is TCP port 8080. The port can be customized via the Gitlab configuration file. The Gitlab process must also be able to initiate communication to PostgreSQL and Redis.
> 
> _If not using the omnibus package, make sure that Redis and PostgreSQL are up and available prior to starting Gitlab_

## Installation

Gitlab can be installed with Docker or via RPM package.

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

Once the repository is configured properly, you can install the Gitlab component using the command:

```bash
sudo yum install stoplight-gitlab -y
```

### Docker Installation

To install the app component with Docker, run the command below:

```bash
docker pull quay.io/stoplight/gitlab
```

> Note, if you have not already authenticated with the Stoplight container registry, you will be prompted for credentials

## Configuring and Running

To configure the Stoplight Gitlab component, you will need to provide connection details to the other necessary components.

### Package-based Installations

#### Configuring the Service

The Stoplight Gitlab configuration is located at:

```bash
/etc/gitlab/gitlab.rb
```

The above file encompasses all of the different configuration options exposed by Gitlab. This guide only covers those specific to Stoplight.

> For documentation on other Gitlab configuration options, please see the official documentation [here](https://docs.gitlab.com/omnibus/README.html#configuring)

#### Starting the Service

To start Gitlab for the first time, run the commands:

```bash
# one-time configuration (needed on new installs and upgrades)
sudo gitlab-ctl reconfigure

# start the services
sudo gitlab-ctl start
```

Once started, you can see the status of the service using the command:

```bash
sudo gitlab-ctl status
```

### Docker Installations

#### Configuring the Container

The Gitlab container should be configured nearly identically to the package installation described above, via file. The easiest way to do this is to mount the Gitlab configuration directory inside the container.

To mount the configuration inside the container, use the `-v` argument to the `docker run` command:

```bash
docker run -v /data/gitlab-config:/etc/gitlab ...
```

Where `/data/gitlab-config` is a directory containing your `gitlab.rb` configuration file.

> See [here](https://docs.gitlab.com/omnibus/README.html#configuring) for more information on how to configure Gitlab

#### Starting the Container

To start the app container, run the command:

```bash
docker run \
        --restart on-failure \
		-v /my/config:/etc/gitlab \
		-p 8080:8080 \
		quay.io/stoplight/gitlab:latest
```

If started properly, the container should be marked with a healthy status within 90 seconds (sometimes a little longer on first boot). Use the `docker ps` command to verify the container was started and is running properly.

## Post-install Validations

Once the Gitlab component is running, you can verify the installation was successful by using the methods below.

### Gitlab Environment Check

Gitlab comes with it's own check that can be useful for catching any improperly configured components. To run this check, use the command:

```bash
sudo gitlab-rake gitlab:check RAILS_ENV=production
```

If you are using a from-source installation, the command is modified to:

```bash
sudo -u git -H bundle exec rake gitlab:check RAILS_ENV=production
```

### Gitlab UI

If the environment check is successful, then you are ready to load up the Gitlab UI. In a web browser, visit the host and port that you are running Gitlab's HTTP port on.

For example, if you are running Gitlab on host `gitlab.example.com` on port `8080`, you can visit the following URL in a web browser to see the Gitlab UI:

[http://gitlab.example.com:8080/](http://gitlab.example.com:8080/)

If the installation was successful, you will be greeted by a Gitlab-branded login screen similar to what is displayed on their [hosted login screen](https://gitlab.com/users/sign_in).

> If you have enabled SSL, be sure to use `https://` when typing the Gitlab URL.

## FAQ


#### Can I use the embedded Redis or PostgreSQL for other services?

Yes! To expose the embedded Redis instance to the outside world, use the configuration:

```ruby
redis['bind'] = '127.0.0.1'
redis['port'] = 6379
```

Similarly, for PostgreSQL, use the configuration:

```ruby
postgresql['listen_address'] = '127.0.0.1'
postgresql['port'] = 5432
```

Once the configuration changes are made, issue a `gitlab-ctl reconfigure` for the changes to take effect.

> If running Gitlab in Docker, be sure to expose the Redis/PostgreSQL ports with the `-p` command-line option

For more information on configuring Redis, please see the official Gitlab documentation [here](https://docs.gitlab.com/omnibus/settings/redis.html).
