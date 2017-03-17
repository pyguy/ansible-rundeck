Role Name
=========

Installs rundeck http://rundeck.org/ role.
Also installs Ansible for executing playbooks and etc. Configurable options and Logstash plugin ready.

Build Status
------------

[![Build Status](https://travis-ci.org/mrlesmithjr/ansible-rundeck.svg?branch=master)](https://travis-ci.org/mrlesmithjr/ansible-rundeck)

Requirements
------------

None

Vagrant
-------
````
vagrant up
````

Usage
-----

Open up browser of choice

Vagrant Environment
http://127.0.0.1:4440
````
user: admin
password: admin
````

Non-Vagrant Environment
http://iporhostname:4440
````
user: admin
password: admin
````

Role Variables
--------------

````
---
# defaults file for ansible-rundeck
config_rundeck: true
enable_rundeck: true
enable_rundeck_plugins: true
pri_domain_name: example.org
rundeck_base: /var/lib/rundeck
rundeck_ssh_generate_key: omit # uses Ansible defaults
rundeck_ssh_keydir: './ssh_pub_keys/'
rundeck_ssh_key_bits: omit # uses Ansible defaults
rundeck_ssh_key_comment: omit # uses Ansible defaults
rundeck_ssh_key_passphrase: omit # uses Ansible defaults
rundeck_ssh_key_type: omit # uses Ansible defaults
rundeck_configs:
  - 'framework.properties'
  - 'rundeck-config.properties'
rundeck_rdeck_jvm: '$RDECK_JVM -Xmx1024m -Xms256m -XX:MaxPermSize=256m -server'
rundeck_mysql_backend: false
rundeck_db_name: 'rundeck'
rundeck_db_host: 'localhost'
rundeck_db_pass: 'rundeck'
rundeck_db_user: 'rundeck'
rundeck_dl_pkg: 'rundeck-{{ rundeck_version }}-GA.deb'
rundeck_dl_url: 'http://dl.bintray.com/rundeck/rundeck-deb/'
rundeck_enable_logstash_plugin: false
rundeck_framework_server_hostname: 'localhost'
rundeck_framework_server_name: 'localhost'
rundeck_framework_server_password: 'admin'
rundeck_framework_server_port: 4440
rundeck_framework_server_url: 'http://{{ rundeck_framework_server_hostname }}'
rundeck_framework_server_username: 'admin'
rundeck_framework_ssh_keypath_file: '{{ rundeck_framework_ssh_keypath }}/id_rsa'
rundeck_framework_ssh_keypath: '/var/lib/rundeck/.ssh'
rundeck_framework_ssh_user: 'rundeck'
rundeck_grails_protocol: 'http'
rundeck_grails_serverURL: "{{ ansible_fqdn }}"
rundeck_grails_port: '4440'
rundeck_jetty_connector_forwarded: false
rundeck_framework_tokens_path: "{{ rundeck_root_dir }}"
rundeck_framework_tokens_file: 'tokens.properties'
# rundeck_framework_tokens:
#  - user: admin
#    key: myRKHyaGJOy5dt61cxyzHq9is0zpCKoq
#  - user: deployer
#    key: S2CbjdRgfADGbxnE4m3yx0xEUFSgVV2N
rundeck_auth_ldap_config: false
rundeck_auth_ldap_debug: 'true'
rundeck_auth_ldap_contextFactory: 'com.sun.jndi.ldap.LdapCtxFactory'
rundeck_auth_ldap_providerUrl: 'ldap://server:389'
rundeck_auth_ldap_authenticationMethod: 'simple'
rundeck_auth_ldap_forceBindingLogin: 'false'
rundeck_auth_ldap_forceBindingLoginUseRootContextForRoles: 'false'
rundeck_auth_ldap_bindDn: 'cn=Manager,dc=example,dc=com'
rundeck_auth_ldap_bindPassword: 'secret'
rundeck_auth_ldap_userBaseDn: 'ou=People,dc=test1,dc=example,dc=com'
rundeck_auth_ldap_userRdnAttribute: 'id'
rundeck_auth_ldap_userIdAttribute: 'cn'
rundeck_auth_ldap_userObjectClass: 'inetOrgPerson'
rundeck_auth_ldap_roleBaseDn: 'ou=Groups,dc=test1,dc=example,dc=com'
rundeck_auth_ldap_roleNameAttribute: 'roleName'
rundeck_auth_ldap_roleMemberAttribute: 'uniqueMember'
rundeck_auth_ldap_roleObjectClass: 'groupOfUniqueNames'
rundeck_auth_ldap_supplementalRoles: 'user'
rundeck_auth_ldap_cacheDurationMillis: '300000'
rundeck_auth_ldap_reportStatistics: 'true'
rundeck_auth_ldap_nestedGroups: 'false'
rundeck_users:
  - name: peter
    password: peterpass
    roles: user
    state: present # default, can be omitted
  - name: 'marry'
    password: marrypass
    roles: 'user,admin'
    state: absent
  - name: 'karl'
    password: "{{ rundeck_userpass_from_somewhere_else }}"
    roles: 'user,admin'
rundeck_install_ansible: true
rundeck_logstash_host: []  #defines logstash server if used
rundeck_logstash_port: 9700
rundeck_root_dir: '/etc/rundeck'
rundeck_vagrant_install: false  #defines if installing under Vagrant
rundeck_version: '2.6.9-1'
rundeck_install_ansible_version: '2.1.1.0'
# rundeck_aclpolicies:
#   - filename: /etc/myrules.aclpolicy # optional
#     owner: 'rundeck'                 # optional
#     group: 'rundeck'                 # optional
#     mode: '0644'                     # optional
#     content: |
#       description: Admin project level access control. Applies to resources within a specific project.
#       context:
#         project: '.*' # all projects
#       for:
#         resource:
#           - equals:
#               kind: job
#             allow: [create] # allow create jobs
#           - equals:
#               kind: node
#             allow: [read,create,update,refresh] # allow refresh node sources
#           - equals:
#               kind: event
#             allow: [read,create] # allow read/create events
#         adhoc:
#           - allow: [read,run,runAs,kill,killAs] # allow running/killing adhoc jobs
#         job:
#           - allow: [create,read,update,delete,run,runAs,kill,killAs] # allow create/read/write/delete/run/kill of all jobs
#         node:
#           - allow: [read,run] # allow read/run for nodes
#       by:
#         group: admin
#       ---
#       description: Admin Application level access control, applies to creating/deleting projects, admin of user profiles, viewing projects and reading system information.
#       context:
#         application: 'rundeck'
#       for:
#         resource:
#           - equals:
#               kind: project
#             allow: [create] # allow create of projects
#           - equals:
#               kind: system
#             allow: [read,enable_executions,disable_executions,admin] # allow read of system info, enable/disable all executions
#           - equals:
#               kind: system_acl
#             allow: [read,create,update,delete,admin] # allow modifying system ACL files
#           - equals:
#               kind: user
#             allow: [admin] # allow modify user profiles
#         project:
#           - match:
#               name: '.*'
#             allow: [read,import,export,configure,delete,admin] # allow full access of all projects or use 'admin'
#         project_acl:
#           - match:
#               name: '.*'
#             allow: [read,create,update,delete,admin] # allow modifying project-specific ACL files
#         storage:
#           - allow: [read,create,update,delete] # allow access for /ssh-key/* storage content

#       by:
#         group: admin


````

Dependencies
------------

None.

Example Playbook
----------------

#### GitHub
````
---
- hosts: all
  become: true
  vars:
  roles:
    - role: ansible-rundeck
  tasks:
````
#### Galaxy
````
---
- hosts: all
  become: true
  vars:
  roles:
    - role: mrlesmithjr.rundeck
  tasks:
````

License
-------

BSD

Author Information
------------------

Larry Smith Jr.
- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com
