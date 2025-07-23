# update_sshd_config

This module provides a convenient way to manage `sshd_config` entries on remote systems using Ansible.  
It allows you to **add**, **update**, or **remove** specific SSH server configuration options programmatically  
within playbooks — without having to manually edit the file.

## Module Overview

**Module Name:** `sshd_config_manager`

**Collection:** `avryez.sshd_config_manager`

---

## Features

- Ensures idempotent management of `sshd_config` directives
- Supports adding new settings or updating existing ones
- Optionally removes settings not explicitly defined
- Performs safe in-place updates while preserving unrelated configuration

## Installation

You can install this collection from Ansible Galaxy:

```bash
ansible-galaxy collection install avryez.sshd_config_manager
```

## Usage Example
```yaml
- name: Harden SSH configuration
  hosts: all
  become: true
  tasks:
    - name: Basic SSH hardening
      avryez.sshd_config_manager.update_ssh_config:
        max_auth_tries: 3
        permit_root_login: "no"
        password_authentication: false
        pubkey_authentication: true
```

## Module Parameters
| Name                          | Required | Type    | Description                                                                                       | Choices                                                                                 | Default      |
|-------------------------------|----------|---------|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|--------------|
| max_auth_tries                | No       | int     | Maximum number of authentication attempts permitted per connection                                |                                                                                         |              |
| permit_root_login             | No       | str     | Whether root can log in using ssh                                                                 | yes, no, without-password, prohibit-password, forced-commands-only                      |              |
| password_authentication       | No       | bool    | Whether password authentication is allowed                                                        | true, false                                                                            |              |
| pubkey_authentication         | No       | bool    | Whether public key authentication is allowed                                                      | true, false                                                                            |              |
| challenge_response_authentication | No   | bool    | Whether challenge-response authentication is allowed                                              | true, false                                                                            |              |
| protocol                     | No       | int     | SSH protocol version                                                                              | 2                                                                                       |              |
| port                         | No       | int     | SSH port number                                                                                   |                                                                                         |              |
| x11_forwarding               | No       | bool    | Whether X11 forwarding is permitted                                                              | true, false                                                                            |              |
| allow_tcp_forwarding         | No       | bool    | Whether TCP forwarding is permitted                                                              | true, false                                                                            |              |
| allow_agent_forwarding       | No       | bool    | Whether ssh-agent forwarding is permitted                                                        | true, false                                                                            |              |
| gateway_ports                | No       | bool    | Whether remote hosts are allowed to connect to local forwarded ports                              | true, false                                                                            |              |
| permit_tunnel                | No       | bool    | Whether tun device forwarding is allowed                                                         | true, false                                                                            |              |
| client_alive_interval        | No       | int     | Timeout interval in seconds after which server will send a message to client; 0 to disable        |                                                                                         |              |
| client_alive_count_max       | No       | int     | Number of client alive messages sent without response before disconnection                        |                                                                                         |              |
| max_sessions                | No       | int     | Maximum number of open sessions permitted per network connection                                  |                                                                                         |              |
| max_startups                | No       | str     | Maximum number of concurrent unauthenticated connections to SSH daemon                            |                                                                                         |              |
| allow_users                 | No       | str     | Space-separated list of user names allowed to log in                                             |                                                                                         |              |
| deny_users                  | No       | str     | Space-separated list of user names not allowed to log in                                         |                                                                                         |              |
| allow_groups                | No       | str     | Space-separated list of group names allowed to log in                                           |                                                                                         |              |
| deny_groups                 | No       | str     | Space-separated list of group names not allowed to log in                                       |                                                                                         |              |
| log_level                   | No       | str     | SSH daemon log level                                                                             | QUIET, FATAL, ERROR, INFO, VERBOSE, DEBUG, DEBUG1, DEBUG2, DEBUG3                       |              |
| syslog_facility             | No       | str     | Syslog facility code for SSH daemon                                                             | DAEMON, USER, AUTH, LOCAL0, LOCAL1, LOCAL2, LOCAL3, LOCAL4, LOCAL5, LOCAL6, LOCAL7       |              |
| use_pam                     | No       | bool    | Whether to use PAM for authentication                                                           | true, false                                                                            |              |
| print_last_log              | No       | bool    | Whether to print the date and time of the last user login                                       | true, false                                                                            |              |
| tcp_keep_alive              | No       | bool    | Whether to send TCP keepalive messages                                                          | true, false                                                                            |              |
| compression                 | No       | bool    | Whether compression is allowed                                                                  | true, false                                                                            |              |
| permit_empty_passwords      | No       | bool    | Whether to allow empty passwords for SSH login                                                  | true, false                                                                            |              |
| login_grace_time            | No       | str     | Time allowed for successful login before disconnecting; can be seconds or time units like '30s'  |                                                                                         |              |
| ignore_rhosts               | No       | bool    | Whether to ignore .rhosts and .shosts files for authentication                                  | true, false                                                                            |              |
| banner                      | No       | str     | Path to the file containing the SSH login banner message                                        |                                                                                         |              |
| hostbased_authentication    | No       | bool    | Whether to allow authentication using host-based authentication                                 | true, false                                                                            |              |
| rhosts_rsa_authentication   | No       | bool    | Whether to allow authentication using Rhosts RSA authentication                                 | true, false                                                                            |              |
| permit_user_environment     | No       | bool    | Whether to allow users to set environment variables                                             |                                                                                         |              |
| subsystem                   | No       | str     | Defines a subsystem such as SFTP                                                               | e.g. `sftp /usr/lib/openssh/sftp-server`                                              |              |
| use_dns                     | No       | bool    | Whether to perform reverse DNS lookups on client IPs                                           | true, false                                                                          |              |
| permit_tty                  | No       | bool    | Whether TTY allocation is permitted                                                            | true, false                                                                          |              |
| force_command               | No       | str     | Forces execution of a specific command after login                                             | Any valid shell command                                                              |              |
| authorized_keys_file        | No       | str     | Location(s) of the user's public key file(s)                                                   | e.g. `.ssh/authorized_keys .ssh/authorized_keys2`                                    |              |
| permit_user_rc              | No       | bool    | Whether to allow user-specific shell rc files (e.g. `~/.ssh/rc`)                               | true, false                                                                          |              |
| stream_local_bind_unlink    | No       | bool    | Whether to remove existing socket file before binding when using Unix domain sockets           | true, false                                                                          |              |
| rekey_limit                 | No       | str     | Maximum amount of data or time before SSH rekeys connection                                    | e.g. `1G`, `1h`, `512M 2h`                                                            |              |
| login_defs                  | No       | bool    | Whether to honor system-wide `/etc/login.defs` settings                                        | true, false                                                                          |              |
| config_file                 | No       | path    | Path to SSH daemon configuration file                                                          |                                                                                         | /etc/ssh/sshd_config |
| backup                      | No       | bool    | Whether to create a backup of the configuration file                                           | true, false                                                                            | true         |
| backup_dir                  | No       | path    | Directory to store backup files                                                                 |                                                                                         | /etc/ssh     |
| validate                    | No       | bool    | Whether to validate SSH configuration after changes                                            | true, false                                                                            | true         |
| restart_service             | No       | bool    | Whether to restart SSH service after successful changes                                        | true, false                                                                            | false        |
| service_name                | No       | str     | Name of the SSH service to restart                                                             |                                                                                         | ssh          |
| gssapi_authentication        | No       | bool    | Whether GSSAPI-based user authentication is allowed                                              | true, false                                                                            |              |
| kerberos_authentication      | No       | bool    | Whether Kerberos authentication is allowed                                                      | true, false                                                                            |              |
| ignore_user_known_hosts       | No       | bool    | Whether to ignore the user's known hosts file                                                    | true, false                                                                            |              |

## Return Values

| Name             | Description                                               |
|------------------|-----------------------------------------------------------|
| `changed`        | Boolean indicating if any changes were made to the config |
| `config_valid`   | Boolean indicating if the final sshd config passed validation |
| `backup_file`    | Path to the backup file created (if backup enabled)       |
| `msg`            | Informational message about what was changed or errors     |
| `changes`        | List of strings describing individual setting changes      |
| `service_restarted` | Boolean indicating if SSH service was restarted           |

## Requirements

- Target host must be running **OpenSSH server**  
- Module tested primarily on **RHEL-based systems**, but should work on other Linux distros with OpenSSH  
- `systemctl` or `service` must be available on the target host if `restart_service` is enabled  
- Python 3.x on the control and managed nodes  
- Ansible 2.10 or later  
