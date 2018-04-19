# Backups

Backups are a critical component to ensuring the health of the Stoplight
platform. When creating a backup and restore strategy for your on-premise
installation, be sure to include the following locations:

* The **GitLab data directory**, which includes the raw filesystem data backing each projects Git repository.
* The **GitLab configuration directory**, which includes randomly-generated secrets and keys necessary for securing the GitLab runtime.
* The **GitLab PostgreSQL database**, which includes user, group, permissions, and other relational data not included in the Git repositories.
* The **Pubs data directory**, which includes published hubs and their corresponding configurations.

Backing up all locations above will ensure you can properly restore a Stoplight
installation without data loss.

## GitLab Backup Procedures

GitLab is a critical piece of the Stoplight platform. Stoplight recommends, at a
minimum, daily backups of the GitLab database and filesystem to ensure minimal
data loss in the event of a failure.

To run a backup for GitLab, which includes a snapshot of the filesystem and
database, run the command:

```bash
sudo gitlab-rake gitlab:backup:create
```

Backups are in zip format, making them very easy to store in remote or cloud
storage. GitLab also offers built-in capabilities that provide automatic uploads
to cloud storage providers when configured.

> If you do not use the built-in backup utility, it is critical that _both_ the
> PostgreSQL database and filesystem data (including data directories and
> configuration directories) be recorded.

For more information, please see the official GitLab backup documentation
[here](https://docs.gitlab.com/ce/raketasks/backup_restore.html).

## Pubs Backup Procedures

Pubs stores all published hubs created via the Stoplight application. While not
critical to the health of the Stoplight Enterprise platform, it is recommended
that the pubs data directory is backed up on a regular basis.

To perform a backup of the Pubs data directory, take a tarball snapshot of the
Pubs data directory and configuration directory. By default, the Pubs data
directory is located at `/var/lib/pubs`, and the configuration directory is
located at `/etc/pubs`.

To perform a backup, run the command:

```bash
sudo tar -cvzf pubs-backup.$(date +%s).tar.gz /var/lib/pubs /etc/pubs
```

Once the backup is completed, the tarball output can be stored on redundant or
cloud storage. To ensure you have a recent backup available at all times,
Stoplight recommends taking a backup daily.
