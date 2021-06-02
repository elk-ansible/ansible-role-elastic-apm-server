Role Name
=========

Ansible Role for Elasticsearch APM server

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

Elastic-Kibana Cluster with x-pack and password set for the `apm_system` user. 
Kibana and Elasticsearch are using the same PKCS12 file for the htts communication.

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
            apm_kibana_user: kibana_system
            apm_kibana_pass: "{{kibana_system_pass}}"
            es_output_ssl_ca: "files/certs/es.example.com.ca"
            es_output_hosts: ["es1:9200","es2:9200"]
            es_output_user: elastic
            es_output_pass: changeme
            es_version: 7.12.1
            es_mon_host: ["es1-mon:9200","es2-mon:9200","es3-mon:9200",]
            es_mon_user: apm_system
            es_mon_pass: "{{apm_system_pass }}"
            apm_ssl_key: "files/certs/es.example.com.key"
            apm_ssl_key_pass: "{{cert_pass}}"
            apm_ssl_cert: "files/certs/es.example.com.crt"



SSL Certificates How To
-------
1. Generate Cert and Key file from PCS12
```shell
export cert_file=es1.dev.example.com.pfx
export KEY_PASS=changeme
openssl pkcs12 -in $cert_file -nocerts -nodes  -out  ${cert_file%.pfx}.key -passin "pass:${KEY_PASS}" -passout "pass:${KEY_PASS}"
openssl pkcs12 -in  $cert_file -clcerts -nokeys -out  ${cert_file%.pfx}.crt -passin "pass:${KEY_PASS}"
```

2. Get the OpenSSL CA file
```shell
openssl s_client -showcerts -connect es1.dev.example.com:9200 </dev/null 2>/dev/null|openssl x509 -outform PEM >es.example.com.ca
```            
Example Playbook For Removing APM Server
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts:  apm-server-node
      tasks:
        - service:
            name: apm-server.service
            state: stopped
          become: true
        - yum:
            name: apm-server
            state: absent
          become: true
        - ansible.builtin.systemd:
            daemon_reexec: yes
          become: true
        - file:
            path: "{{item}}"
            state: absent
          with_items:
            - /etc/apm-server
            - /usr/share/apm-server
            - /var/lib/apm-server
          become: true
    





License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
