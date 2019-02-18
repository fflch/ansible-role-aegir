# Ansible Role: Aegir

[![Build Status](https://travis-ci.org/ergonlogic/ansible-role-aegir.svg?branch=master)](https://travis-ci.org/ergonlogic/ansible-role-aegir)

Installs Aegir, a control panel for deploying and managing large networks of Drupal sites.

## Requirements

 - php with version according the needs of yours platforms
 - php extensions required by Drupal
 - composer
 - apache or nginx
 - mysql

A MySQL server is required. This server can be installed on the same machine,
or a separate one (hence why this isn't listed as a dependency.) See the
'Example Playbook' section below for a simple method of installing a mysql
server with Ansible. If this role is not present, then the
`mysql_root_username`and `mysql_root_password` variables must be set.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    aegir_db_username: "{{ mysql_root_username }}"

The name of the Aegir database user. Defaults to the value of mysql_root_username.

    aegir_db_password: "{{ mysql_root_password }}"

The password for the Aegir database user. Defaults to the value of mysql_root_password.


## Dependencies

- ergonlogic.drush (Installs Drush).

## Example Playbook

    - name: deploy aegir with ansible
      hosts: aegir

      vars:

        # geerlingguy.php-versions
        php_version: '7.2'

        # geerlingguy.php
        php_default_version_debian: '7.2'
        php_use_managed_ini: false
        php_packages_extra:
          - php{{ php_default_version_debian }}-mysql

        # aegir role
        aegir_additional_packages:
          - libapache2-mod-php{{ php_default_version_debian }}

      roles:
        - geerlingguy.mysql
        - geerlingguy.apache
        - geerlingguy.php-versions
        - geerlingguy.php
        - geerlingguy.composer
        - aegir

After the playbook runs, the Aegir front-end site will be available, as will
the Drush extensions (Provision, et. al.) that do the heavy lifting.

## License

MIT / BSD

## Author Information

This role was created in 2015 by [Christopher Gervais](http://ergonlogic.com/), lead maintainer of the [Aegir Hosting System](http://www.aegirproject.org).
