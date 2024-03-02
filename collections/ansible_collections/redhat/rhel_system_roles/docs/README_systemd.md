# systemd


Ansible role that can be used to deploy unit files and manage systemd units. Role is a convenience
wrapper around systemd and template Ansible Core modules.

## Role Variables

List of variables consumed by the role follows, note that none of them is mandatory.

### systemd_unit_files

List of systemd unit file names that should be deployed to managed nodes.

### systemd_unit_file_templates

List of systemd unit file names that should be deployed to managed nodes. Each name should
correspond to Jinja template file that will be templated out to managed nodes, e.g. for unit
`foo.service` the respective `foo.service.j2` will be templated and copied over to managed
nodes.  If the local file has a `.j2` suffix it will be stripped to form the service name.

### systemd_dropins

List of systemd drop in files that will be templated out to managed hosts and will extend
respective systemd unit files. Name of the unit file that given entry extends is encoded in
the name of the entry itself. For example, for entry `foo.service.conf` it is expected that
`foo.service.conf.j2` Jinja template exists and resulting dropin file will extend `foo.service`
unit file.  If the local file has a `.j2` suffix it will be stripped to form the service
name.

### systemd_started_units

List of unit names that shall be started via systemd.

### systemd_stopped_units

List of unit names that shall be stopped via systemd.

### systemd_restarted_units

List of unit names that shall be restarted via systemd.

### systemd_reloaded_units

List of unit names that shall be reloaded via systemd.

### systemd_enabled_units

List of unit files that shall be enabled via systemd.

### systemd_disabled_units

List of unit files that shall be disabled via systemd.

### systemd_masked_units

List of unit files that shall be masked via systemd.

### systemd_unmasked_units

List of unit files that shall be unmasked via systemd.

Example of setting the variables:

```yaml
systemd_unit_files:
  - foo.service
  - bar.service
systemd_dropins:
  - cups.service.conf.j2
  - avahi-daemon.service.conf.j2
systemd_started_units:
  - foo.service
  - bar.service
systemd_enabled_units:
  - foo.service
  - bar.service
```

## Variables Exported by the Role

### `systemd_units`

Variable shall contain a list of dictionaries where each entry describes state of one systemd unit
present on the managed host.

## Example Playbook

Including an example of how to use your role (for instance, with variables
passed in as parameters) is always nice for users too:

```yaml
- name: Deploy and start systemd unit
  hosts: all
  vars:
    systemd_unit_files:
      - foo.service
    systemd_started_units:
      - foo.service
    systemd_enabled_units:
      - foo.service
  roles:
    - redhat.rhel_system_roles.systemd
```

## License

MIT

## Author

Michal Sekletar <msekleta@redhat.com>
