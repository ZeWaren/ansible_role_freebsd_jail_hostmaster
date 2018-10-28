# ansible-freebsd-jail-hostmaster

## Introduction
This role configures jails on a FreeBSD server, using `ezjail` and `ZFS`.

Use it at your own risks.

## Variables

### ezjail_jailzfs

Which ZFS dataset should hold the jails.

### jailed_zfs_endpoint

The ZFS datasets that must be set as `jailed`. (only if you have jails that use ZFS).

### jails

The list of jails.

### jails.name

The name of the jail.

### jails.hostname

The hostname of the jail.

### jails.ip_address

The list of IP address of the jail.

### jails.started

Whether or not the jail should be started.

### jails.parameters

The jails parameters.

### jails.zfs_datasets

Which ZFS datasets should be available into the jail.

### jails.start_ssh

If true, then sshd will be enabled and started inside the jail, and the SSH public key used to connect to the hostmaster is copied into the home directory of user `ansible`, so that the new jail can be provisioned immediately after.

### jails.use_sudo

If true, install sudo and allow group `wheel` and user `ansible` to use it inside the jail.

### jails.exec_stop

If set, configure which command is run inside the jail before stopping it.

### jails.enable_zfs_acls

If set, then the jails dataset will be allowed to use ACLs.

### jails.started_after

If set, ensure a list of jails is started before this one.

## Example

ezjail_jailzfs: zroot/jails
jails:
  - name: "example_com"
    hostname: "example.com"
    ip_address: "10.4.2.150"
    started: yes
    parameters: allow.raw_sockets allow.socket_af securelevel=3
    start_ssh: yes
    use_sudo: yes
  - name: "example_net"
    hostname: "example.net"
    ip_address: "10.4.2.155,10.4.2.156"
    started: yes
    parameters: allow.raw_sockets allow.socket_af securelevel=3
    start_ssh: yes
    use_sudo: yes

## Dependencies

None.

## Licence

BSD

## Author

[Erwan Martin](https://zewaren.net/)
