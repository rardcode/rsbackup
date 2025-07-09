# RsBackup
Script for take system backup using Rsync.

## INSTALLATION:
```
cd /opt
git clone https://github.com/rardcode/rsbackup.git
ln -s /opt/rsbackup/rsbackup /usr/local/bin/
```

## USAGE:
1. Launch `rsbackup -b <hostname>` for make needed files in `/root/.rsbackup` (`config_<hostname>` & `exclusion_<hostname>`;

2. NOTE: form more backup in the same hostname, use `<hostname-xxx>` & add new entry in /etc/host of the backup server. Ex: hostname = localhost-var, add `127.0.0.1  hostname-var` in /etc/hosts;

3. (optional) - Edit `config_<hostname>` with preferred env value as dest mail, ssh user, backup numbers to keep;
4. (optional) -> Edit `exclusions_<hostname>` with path to be exclude/include;

5. **IMPORTANT**: if the `<hostname>` is remote, launch `ssh-copy-id root@<hostname>` in the backup server for copy local key and permit the automatic ssh connection;

6. Launch `rsbackup -b <hostname>`.

7. REPORT: if `mail` command is installed, this script will use it & you will receive a more detailed report: check config of your Postfix or other MTA. Customize `$SRC_MAIL` & `$DEST_MAIL` envs in `config_<hostname>` file.

8. IMPORTANT: Log rotation:\
add `/var/log/backup/*.log` in\
`/etc/logrotate.d/rsyslog` (Debian) or in\
`/etc/logrotate.d/syslog-ng` (Manjaro) or in\
`/usr/etc/logrotate.d/syslog` (OpenSUSE)

9. (optional) - Insert command in crontab with only desidered time:\
     `echo "00 00 * * * /root/bin/rsbackup -b <hostname>" >> /var/spool/cron/root`

10. (optional) - You can also use `.rsync-exclude` file in dir where you have to exclude some files/dirs.\
     USAGE: Insert in `.rsync-exclude` entire name or using wildcard:\
     Ex. Content of `.rsync-exclude` file:\
     file*\\\
     file2\\\
     *file3

     or put simply wildcard(*) for all content dir.

## UPGRADE:
```
cd /opt
git clone https://github.com/rardcode/rsbackup.git
```
