# GitLab Backup Procedures

GitLab is a critical piece of the Stoplight Enterprise platform. Stoplight
recommends, at a minimum, daily backups of the GitLab database and filesystem to
ensure minimal data loss in the event of a failure.

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

# Pubs Backup Procedures

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
cloud storage.
