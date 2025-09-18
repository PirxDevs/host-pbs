# Host backup and restore scripts

These scripts enable you to back up and restore your Linux system to and from the Proxmox Backup Server.

Before using them, copy the file "host-pbs.example.conf" to "host-pbs.conf," and then review and edit it to match your configuration and needs.

## host2pbs

This script will back up the host's root file system. By default, other file systems and mount points will not be included. Use the -a option to include all mount points, except for pseudo file systems such as /dev, /proc, and /sys. You can also define additional includes or excludes in pbs2host.conf.

To run the backup, simply run the script, or preferrably, add it to the cron job. You can first run it with the -d option for a dry run to see what will be done.

## pbs2host

This script allows you to restore files from a backup. Simply run the script, and it will return a list of available backup groups (hosts).

```
# ./pbs2host
Available backup groups:

host/some.server.com
host/other.server.net
```

Add the desired group name as an option to the script, then run it again. It will list the available snapshots for the given backup group.

```
# ./pbs2host host/some.server.com
Available backup snapshots for group host/some.server.com:

2025-05-25T05:20:25Z
2025-06-25T05:03:13Z
```

Add the snapshot name as an option to the script, along with the path in which the restored files should be saved. For example:

`./pbs2host host/some.server.com 2025-05-25T05:20:25Z /mnt/restored-files`

You can restore only specific paths by adding them as script options. For example, to restore only /etc and /root, do the following:

`./pbs2host host/some.server.com 2025-05-25T05:20:25Z /mnt/restored-files /etc /root`
