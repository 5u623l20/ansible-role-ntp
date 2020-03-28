# Ansible Role for ntp or time synchronization

Ansible Role for ntp or time synchronization service on *nix alike OS

# Requirements

If it is required to use `ntp_restrict` with Debian/Ubuntu/FreeBSD based systems please install Python `netaddr` module like the following for Ansible HOST only:
```shell
pip install netaddr
```

# Role Variables

vailable variables which can be called during runtime are listed below with their default values (see `defaults/main.yml`):

```yaml
ntp_enabled: true
```

Whether to enable ntpd service. It's advisable not to run ntpd service on Kernel based Desktop based virtualization guests, since the host itself should be set to synchronize time for all its child VMs.

```yaml
ntp_timezone: Etc/UTC
```

Configures the timezone of the server.

```yaml
ntp_package: ntp
```

Package to provide ntp functionality. Default is set to ntp. For CentOS chrony is used and for FreeBSD default ntpd from base system is used.

```yaml
ntp_pools: []
```

Set the [NTP Pool Area](http://support.ntp.org/bin/view/Servers/NTPPoolServers) to use. Defaults to none, which uses the default OS configured worldwide pool.

```yaml
ntp_servers: []
```

Specify the ntp servers if there is any available in the local network. Rather than using the NTP Worldwide Pool it is advisable to use a local one which synchronizes with the NTP Pools. ntp_servers take precedence over ntp_pools.

```yaml
ntp_restrict: []
```

By default only `127.0.0.1` and `::1` is allowed to query the host. If any local network needs to be allowed it should be added in CIDR format(e.g `192.168.0.0/24`).

```yaml
ntp_daemon: ntp
```

NTP daemon used to start/stop the service. Nothing to configure.

```yaml
ntp_tzdata_package: tzdata
```

Package to provide updated time definitions.

```yaml
drift_file: /var/lib/ntp/ntp.drift
```

NTP drift file location used in configuration file.

```yaml
leap_file: /usr/share/zoneinfo/leap-seconds.list
```

NTP leap-seconds file location. Nothing to configure.

# Dependencies

None.

# Example Playbook

```yaml
- hosts: alls
  roles:
    - 5u623l20.ntp
    vars:
      ntp_timezone: Etc/UTC+6
      ntp_pools:
        - 0.bd.pool.ntp.org
        - 1.bd.pool.ntp.org
        - 2.bd.pool.ntp.org
```

# License
BSD-3-CLAUSE

Author Information
------------------
Created in 2020 by [Muhammad Moinur Rahman](https://bofh.am)


---
