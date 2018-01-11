java
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-java.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-java)

Provides java (oracle or openjdk), jre or jdk, versions 6, 7, 8 or 9 for many distributions:
- Alpine
- CentOS
- Debian
- Fedora
- Ubuntu

Requirements
------------

- For openjdk: Access to a repository containing packages, likely on the internet.
- For oracle: Download the rpms and/or tar.gz's from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/index.html) and place then in the "files" directory. These files are not included because a license has to be accepted. For each version download the "jre" and "jdk", x64 version.

Role Variables
--------------

- java_version: 6, 7, 8 or 9, defaults: 7
- java_vendor: openjdk or oracle, default: openjdk
- java_type: jdk or jre, default: jre
- java_format: rpm or targz, default: targz. (only applicable for java_vendor: oracle)
- java_install_directory: for targz installations, default: /opt. (only applicable for java_vendor: oracle)
- java_jce: "yes" if you want to install the Java Cryptography Extension, default: unset (only applicable for java_vendor: oracle and java_version: 8)

Have a look in vars/main.yml to see all available combinations.

Dependencies
------------

- robertdebock.bootstrap

Download the dependencies by issuing this command:
```
ansible-galaxy install --role-file requirements.yml
```

Example Playbooks
----------------

For a default installation (defaults in defaults/main.yml) use this playbook:
```
- hosts: servers
  gather_facts: yes
  become: yes

  roles:
    - role: robertdebock.java
```

For an installation of Oracle jdk version 9, use this playbook:
```
- hosts: servers
  gather_facts: yes
  become: yes

  roles:
    - role: robertdebock.java
      java_vendor: oracle
      java_type: jdk
      java_version: 9
      java_format: rpm
```

Install this role using `galaxy install robertdebock.java`.

License
-------

Apache License, Version 2.0

Author Information
------------------

Robert de Bock <robert@meinit.nl>
