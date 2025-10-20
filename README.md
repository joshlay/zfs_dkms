# zfs\_dkms

Ansible Role for [ZFS](https://zfsonlinux.org/) on
[Fedora](https://openzfs.github.io/openzfs-docs/Getting%20Started/Fedora/index.html),
[Red Hat](https://openzfs.github.io/openzfs-docs/Getting%20Started/RHEL-based%20distro/index.html)/derivatives,
[Debian](https://openzfs.github.io/openzfs-docs/Getting%20Started/Debian/index.html),
or [Ubuntu](https://openzfs.github.io/openzfs-docs/Getting%20Started/Ubuntu/index.html).

## Role Variables

| Variable | Description | Role Default | Upstream Default |
|----------|:------------|-------------:|-----------------:|
| `zfs_dkms_arc_pct_min` | _Minimum_ physical memory (%) for ARC.<br />_(Adaptive Read Cache)_ | `0` | `0` |
| `zfs_dkms_arc_pct_max` | _Peak_ physical memory (%) for ARC. | `16` | `0` |
| `zfs_dkms_timeout` | Seconds to wait while rebooting `Fedora`, `RHEL`, or derivatives for kernel/header currency. Not applicable to `Debian` or `Ubuntu`.<br /><br />Skipped when `zfs` is already loaded. | `3600` | _N/A_ |

## Dependencies

1. `community.general`: use modules `rhsm_repository`, `dnf_config_manager`, and `modprobe`

## Example Playbook

```yaml
---
- name: ZFS + Pool
  hosts: all
  vars:
    zfs_mirror_disks:  # see NOTE below
      - /dev/disk/by-id/ata-WDC_WD120EFBX-ABCDEFG_12345678
      - /dev/disk/by-id/ata-WDC_WD120EFBX-HIJKLMN_87654321
  roles:
    - name: zfs_dkms  # this role, installs/builds ZFS
      vars:
        zfs_dkms_arc_pct_max: 33
  tasks:
    - name: "Pool (mirror, 'rust')"  # see also: 'community.general.zfs'
      when: zfs_mirror_disks is defined
      community.general.zpool:
        name: rust
        pool_properties:
          ashift: 12
        filesystem_properties:
          compression: lz4
        vdevs:
          - type: mirror
            disks: "{{ zfs_mirror_disks }}"  # reminder: see NOTE below
      become: true
```

_NOTE:_ **Not** recommended to inline `zfs_mirror_disks`, `zfs_dkms_arc_pct_max`, or _pool/filesystem properties_.
Values are expected to be unique among hosts _[or groups]_.  
Use the
[inventory](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html#assigning-a-variable-to-one-machine-host-variables)
or [host/group vars](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html#organizing-host-and-group-variables)
instead.

## License

[MIT](./LICENSE)
