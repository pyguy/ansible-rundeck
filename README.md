# ansible-rundeck

An Ansible role to install [Rundeck](https://www.rundeck.com/)

> NOTE: Also installs Ansible for executing playbooks and etc. Configurable
> options and Logstash plugin ready.

## Requirements

None

## Vagrant

```bash
vagrant up
```

## Usage

Open up browser of choice

[Vagrant Environment](http://127.0.0.1:4440)

```yaml
user: admin
password: admin
```

[Non-Vagrant Environment](http://iporhostname:4440)

```yaml
user: admin
password: admin
```

## Role Variables

[defaults/main.yml](defaults/main.yml)

## Dependencies

None.

## Example Playbook

```yaml
---
- hosts: all
  become: true
  vars:
  roles:
    - role: ansible-rundeck
  tasks:
```

## License

MIT

## Author Information

Hamidreza Joshaghani

-   [@hrjosheghani](https://www.twitter.com/hrjosheghani)
-   <mailto:hr.josheghani@gmail.com>
