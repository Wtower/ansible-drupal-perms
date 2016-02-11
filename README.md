drupal-perms
============

Ansible role to properly configure the permissions of a Drupal site.

Add the role `drupal-perms` (see examples).

Variables:

- `drupal_sites`: Configuration dictionary
- `site`: Index in `drupal_sites` to the particular Drupal site
- `ansible_user_id`: The user id with access to mysql and mysql database
- `apache_user`: The apache user

Playbook examples
-----------------

Configuration file:

    ---
    drupal_sites:
      site.com:
        staging:
          path: /var/www/vhosts/site.com/httpdocs
          alias: site.dev-p5qc
        prod:
          path: /var/www/vhosts/site.com
          alias: site.com

Playbook:

    ---
    # Set Drupal permissions
    #
    # Extra variables:
    # - host: provide the local staging host
    # - site: provide the site from conf to sync
    # - dest: staging/prod
    #
    # Optional extra variables
    # - ansible_user_id: default defined in group_vars
    # - apache_group: default is www-data, optionally plesk
    #
    # Example: ansible-playbook drupal_perms.yml -e "host=dev-p5qc site=a.gr dest=staging"
    
    - hosts: "{{ host }}"
      gather_facts: no
    
      vars_files:
        - ../conf/drupal_sites.yml
    
      roles:
        - drupal_perms
    