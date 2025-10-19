# zfs\_dkms

Ansible Role for the [ZFS](https://zfsonlinux.org/) kernel module
on [Fedora](https://openzfs.github.io/openzfs-docs/Getting%20Started/Fedora/index.html),
[Red Hat](https://openzfs.github.io/openzfs-docs/Getting%20Started/RHEL-based%20distro/index.html)/derivatives,
[Debian](https://openzfs.github.io/openzfs-docs/Getting%20Started/Debian/index.html),
or [Ubuntu](https://openzfs.github.io/openzfs-docs/Getting%20Started/Ubuntu/index.html).
For pools/volumes, see:

1. [community.general.zpool](https://docs.ansible.com/ansible/latest/collections/community/general/zpool_module.html)
2. [community.general.zfs](https://docs.ansible.com/ansible/latest/collections/community/general/zfs_module.html)

## Requirements

None.

## Role Variables

| Variable | Description | Role Default | Upstream Default |
|----------|:------------|-------------:|-----------------:|
| `zfs_dkms_arc_pct_min` | _Minimum_ physical memory (%) for ARC.<br />_(Adaptive Read Cache)_ | `0` | `0` |
| `zfs_dkms_arc_pct_max` | _Peak_ physical memory (%) for ARC. | `16` | `0` |
| `zfs_dkms_timeout` | Seconds to wait while rebooting `Fedora`, `RHEL`, or derivatives for kernel/header currency. Not applicable to `Debian` or `Ubuntu`.<br /><br />Skipped when `zfs` is already loaded. | `3600` | _N/A_ |

## Dependencies

1. `community.general`

## License

MIT
