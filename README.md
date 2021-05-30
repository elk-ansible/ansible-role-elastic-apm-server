Role Name
=========

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - name: Install and Configure Elastic APM Server
      hosts: apm-server
      roles:
      - role: apm-server
        vars:
            apm_server_host: "{{ansible_default_ipv4.address}}"
            apm_kibana_host: "kibana.example.com"
            apm_kibana_user: elastic
            apm_kibana_pass: changeme
            es_output_ssl_ca: "files/certs/es.example.com.ca"
            es_output_hosts: ["es1:9200","es2:9200"]
            es_output_user: elastic
            es_output_pass: changeme
            es_version: 7.12.1
            es_mon_host: ["es1-mon:9200","es2-mon:9200","es3-mon:9200",]
            es_mon_user: elastic
            es_mon_pass: changeme


License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
