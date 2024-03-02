# tlog


This role configures a system for [Terminal session
recording](https://github.com/scribery). The role will configure tlog to log
recording data to the systemd journal.

## Requirements

This role is only supported on RHEL8/CentOS8 and Fedora distributions.

## Role Variables

Configure session recording with SSSD, the preferred way of managing recorded
users or groups. This causes the SSSD files provider to be enabled explicitly.

- `tlog_use_sssd` (default: `true`)

Configure SSSD recording scope - `all` / `some` / `none`:

- `tlog_scope_sssd` (default: `none`)

YAML list of users to be recorded:

- `tlog_users_sssd` (default: `[]`)

YAML list of groups to be recorded:

- `tlog_groups_sssd` (default: `[]`)

YAML list of users to be excluded from recording (only applicable when
scope=all):

- `tlog_exclude_users_sssd` (default: `[]`)

YAML list of groups to be excluded from recording (only applicable when
scope=all):

- `tlog_exclude_groups_sssd` (default: `[]`)

## Example Playbook

```yaml
- name: Deploy session recording
  hosts: all
  roles:
    - redhat.rhel_system_roles.tlog
  vars:
    tlog_scope_sssd: some
    tlog_users_sssd:
      - recordeduser
```

## Testing

Testing is done with the `tests/tests_*.yml` playbooks.  See `contributing.md`.

## License

GPL v3.0

## Author Information

- Nathan Kinder @nkinder

- Kirill Glebov @sabbaka
