[![Build Status](https://travis-ci.org/rajiteh/ansible-role-sysvinit-service.svg)](https://travis-ci.org/rajiteh/ansible-role-sysvinit-service)
[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-sysvinit--service-blue.svg)](https://galaxy.ansible.com/rajiteh/sysvinit-service/)

sysvinit-service - Ansible role
===============

Register services to sysvinit system. 

Install
-------

    $ ansible-galaxy install rajiteh.sysvinit-service


Role Variables
--------------

|name                |type    |default|description
|--------------------|--------|-------|-------------
|`sysvinit_service_name` * |str||service name
|`sysvinit_service_description` * |str||service description
|`sysvinit_service_bin` * |str||path to the service executable
|`sysvinit_service_args`|str|`""`| arguments to the service executable
|`sysvinit_service_user`|str|`root`|user to run the service as
|`sysvinit_service_envs`|list[str] / list[dict]|[]|`/etc/default/:service_name` for each item, if string, will be 
|`sysvinit_default_dir`|str|"/etc/default"|envs file path
|`sysvinit_initd_dir`|str|"/etc/init.d"|init.d path rendered in a new line, if map, will be rendered as key=value in the defaults file.
|`sysvinit_service_runlevels`|int|2345|chkconfig runlevels
|`sysvinit_service_startpriority`|int|80|chkconfig start priority
|`sysvinit_service_endpriority`|int|80|chkconfig end priority
|`sysvinit_service_pid_path`|str|`/var/run/{{ sysvinit_service_name }}.pid`|path to create the pid 
|`sysvinit_service_log_path`|str|`/var/log/{{ sysvinit_service_name }}.log`|path to create the log


> * Required

Example Playbook
----------------

```yaml
- hosts: servers
    roles:
    - role: sysvinit-service
        sysvinit_service_name: node-exporter
        sysvinit_service_description: Prometheus node exporter
        sysvinit_service_bin: /opt/bin/node_exporter
        sysvinit_service_args: "-web.listen-address=:9100"
        sysvinit_service_user: prometheus
        sysvinit_service_envs:
            - SOME_ENV: value
            OTHER_ENV: value
            - "ANOTHER_ENV=value"
```

License
-------

MIT

Author Information
------------------

> @rajiteh