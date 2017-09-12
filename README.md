# jenkins_server

Master: [![Build Status](https://travis-ci.org/sansible/jenkins_server.svg?branch=master)](https://travis-ci.org/sansible/jenkins_server)  
Develop: [![Build Status](https://travis-ci.org/sansible/jenkins_server.svg?branch=develop)](https://travis-ci.org/sansible/jenkins_server)

* [ansible.cfg](#ansible-cfg)
* [Installation and Dependencies](#installation-and-dependencies)
* [Tags](#tags)
* [Examples](#examples)

This roles installs [Jenkins](https://jenkins.io/) for CI/CD. Comes with basic
auth and plugin installation.




## ansible.cfg

This role is designed to work with merge "hash_behaviour". Make sure your
ansible.cfg contains these settings

```INI
[defaults]
hash_behaviour = merge
```




## Installation and Dependencies

To install run `ansible-galaxy install sansible.jenkins_server` or add this to your
`roles.yml`.

```YAML
- name: sansible.jenkins_server
  version: v1.0
```

and run `ansible-galaxy install -p ./roles -r roles.yml`




## Tags

This role uses tags: **build** and **configure**

* `build` - Installs ...
* `configure` - Configures ...




## Examples

Simply include role in your playbook:

```YAML
- name: Install and configure jenkins_server
  hosts: "somehost"

  roles:
    - role: sansible.jenkins_server
```

By default private security will be enabled with an admin user, you can change
the default admin username and password like so:

```YAML
- name: Install and configure jenkins_server
  hosts: "somehost"

  roles:
    - role: sansible.jenkins_server
      jenkins_server:
        basic_auth:
          admin_password: changemechangeme
          admin_username: admin
```

If you want to use another auth plugin then you can disable basic auth like so:

```YAML
- name: Install and configure jenkins_server
  hosts: "somehost"

  roles:
    - role: sansible.jenkins_server
      jenkins_server:
        basic_auth:
          enabled: no
```

Plugins can be installed as well, state and version are optional:

```YAML
- name: Install and configure jenkins_server
  hosts: "somehost"

  roles:
    - role: sansible.jenkins_server
      jenkins_server:
        plugins:
          - name: ansicolor
            state: present
            version: 0.1.2
          - name: git
            version: 3.5.1
          - name: timestamper
            version: 1.8.8
```

Note that if you switch off basic auth then this step will only run on a fresh
installation since this role will not have credentials to authenticate.
