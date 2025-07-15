# Host backup and restore scripts

These scripts enable you to back up and restore your Linux system to and from the Proxmox Backup Server.

Before using them, copy the file "host-pbs.example.conf" to "host-pbs.conf," and then review and edit it to match your configuration and needs.

## host2pbs

This script will back up the root file system of the host on which it is run, including all mount points, except for pseudo file systems, such as /dev and /sys, and any paths listed as excluded in the host-pbs.conf file.

To run the backup, simply run the script, or preferrably, add it to the cron job.

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
