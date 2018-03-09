docker-prometheus
=========

This role creates a docker stack with 4 containers:
* prom/node-exporter
* prom/alertmanager
* prom/prometheus
* grafana/grafana

It will configure a prometheus server to pull metrics from the node exporter. Grafana is then configured to pull those metrics from prometheus trough a file configured datasource. The alert manager is also configured to push alert notifications to an email address of your choosing.

Requirements
------------
**This role does not install docker on the remote host**. You should get another role for that (I do have one, but so far, it sucks, and I shall not make it public. Feel free to recommend an ansible-galaxy dependecy that you trust).


Role Variables
--------------
Read trough the default variable file and report any variable name that is unclear to you. 
You **NEED** to ovewrite the variables int vars/main.yml in order for the notifications to work, and for your grafana to be somewhat secure.

* alert_manager_source_email: gmail account which will be use to send notifications
* alert_manager_source_password: gmail password of the alert_manager_source_email
* grafana_admin_user: the default user of grafana
* grafana_admin_password: the default passowrd of the grafana_admin_user

Two notes:
* the alert_manager_source_email and passowrd should be from gmail if you won't use a personnal smtp server. By default, the role will use gmail's smtp public server.
* While the grafana_admin_user and password variables will change their values on the first run, they won't overwrite if you run the role again, as they appear to be stored in the storage, and no longer red by grafana after the first run. You should change them trough the web interface.

Dependencies
------------


Example Playbook
----------------
Pretty straigh forward.
``` yaml
---
- hosts: localhost
  roles:
    - prometheus-docker
```

License
-------

MIT License

Author Information
------------------

I'm a newly graduate student from Québec. This is my first public role, so feel free to point mishaps and errors.
