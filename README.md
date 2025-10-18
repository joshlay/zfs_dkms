zfs\_dkms
=========

Manages [ZFS on Linux](https://zfsonlinux.org/)
for [Red Hat/derivatives](https://openzfs.github.io/openzfs-docs/Getting%20Started/RHEL-based%20distro/index.html),
[Debian](https://openzfs.github.io/openzfs-docs/Getting%20Started/Debian/index.html),
and [Ubuntu](https://openzfs.github.io/openzfs-docs/Getting%20Started/Ubuntu/index.html)

Requirements
------------

None.

Role Variables
--------------

| Variable | Description | Role Default | Upstream Default |
|----------|:-----------:|--------:|--------:|
| `zfs_dkms_arc_pct_min` | Minimum physical memory (%) allowed for ARC usage | `0` | `0` |
| `zfs_dkms_arc_pct_max` | Max physical memory (%) allowed for ARC usage | `16` | `0` |
| `zfs_dkms_timeout` | Seconds to wait while rebooting `RHEL`/derivatives<br />_[for kernel update and current headers]_ | `3600` | _N/A_ |

Dependencies
------------

1. `community.general`

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: zfs_dkms }

License
-------

Apache-2.0
