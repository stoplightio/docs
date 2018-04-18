# GitLab CE

GitLab CE powers the Stoplight backend, including file storage and database.
GitLab is the backing datastore for all files stored within Stoplight. In
addition to storing files, GitLab is responsible for:

* Interfacing with the Stoplight API
* User-facing notifications (including password reset emails, group/project
  invitations, etc)
* Tracking all changes between different files, and storing them within a Git
  repository

Packaged within the GitLab CE is an embedded installation of PostgreSQL and
Redis. These two sub-components can be broken out into external services if your
organization is already familiar with running these (or similar) services. You
may also break out these services if you plan on using a managed hosting
solution, for example, Amazon RDS (for PostgreSQL) or Amazon ElastiCache (for
Redis).

> #### Storage Requirements
>
> GitLab requires persistent storage in order to store Stoplight file data (in
> Git), and optionally PostgreSQL data (when using the omnibus package).

> #### Networking Details
>
> The default GitLab ports are 80 (HTTP) and 443 (HTTPS). These ports can be
> customized via the `gitlab.rb` configuration file (discussed below).
>
> GitLab must be able to receive incoming connections from the following components:
>
> * App
>
> GitLab must be able to make outgoing connections to the following components:
>
> * PostgreSQL
> * Redis

> #### Component Dependencies
>
> Make sure the following components are available **before** starting the GitLab
> service:
>
> * PostgreSQL
> * Redis
>
> _Note, for Omnibus users using the embedded PostgreSQL and Redis instances,
> these services will be started by the GitLab process._

## Installation

GitLab can be installed with Docker or via RPM package.

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

> Make sure that the repository credentials are set before issuing the `cat` command

Once the repository is configured properly, you can install the GitLab component using the command:

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

To configure the Stoplight GitLab component, you will need to provide connection details to the other necessary components.

### Package-based Installations

#### Configuring the Service

The Stoplight GitLab configuration is located at:

```bash
/etc/gitlab/gitlab.rb
```

The above file encompasses all of the different configuration options exposed by GitLab. This guide only covers those specific to Stoplight.

> For documentation on other GitLab configuration options, see the official
> documentation [here](https://docs.gitlab.com/omnibus/README.html#configuring)

#### Starting the Service

To start GitLab for the first time, run the commands:

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

The GitLab container should be configured nearly identically to the package installation described above, via file. The easiest way to do this is to mount the GitLab configuration directory inside the container.

To mount the configuration inside the container, use the `-v` argument to the `docker run` command:

```bash
docker run -v /data/gitlab-config:/etc/gitlab ...
```

Where `/data/gitlab-config` is a directory containing your `gitlab.rb` configuration file.

> See [here](https://docs.gitlab.com/omnibus/README.html#configuring) for more information on how to configure GitLab

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

Once the GitLab component is running, you can verify the installation was successful by using the methods below.

### GitLab Environment Check

GitLab comes with it's own check that can be useful for catching any improperly configured components. To run this check, use the command:

```bash
sudo gitlab-rake gitlab:check RAILS_ENV=production
```

If you are using a from-source installation, the command is modified to:

```bash
sudo -u git -H bundle exec rake gitlab:check RAILS_ENV=production
```

### GitLab UI

If the environment check is successful, then you are ready to load up the GitLab UI. In a web browser, visit the host and port that you are running GitLab's HTTP port on.

For example, if you are running GitLab on host `gitlab.example.com` on port `8080`, you can visit the following URL in a web browser to see the GitLab UI:

[http://gitlab.example.com:8080/](http://gitlab.example.com:8080/)

If the installation was successful, you will be greeted by a GitLab-branded login screen similar to what is displayed on their [hosted login screen](https://gitlab.com/users/sign_in).

> If you have enabled SSL, make sure to use `https://` when typing the GitLab URL.

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

> If running GitLab in Docker, be sure to expose the Redis/PostgreSQL ports with the `-p` command-line option

For more information on configuring Redis, see the official GitLab documentation
[here](https://docs.gitlab.com/omnibus/settings/redis.html).
