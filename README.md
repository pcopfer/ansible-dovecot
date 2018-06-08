pcopfer.dovecot
==============

A role to manage Dovecot.

Role Variables
--------------

- ``dovecot_fqdn: "{{ ansible_fqdn }}"``
- ``dovecot_domain: "{{ ansible_domain }}"``
- ``dovecot_auth_passwdfile: true`` Use passwordfiles for User, created out of var mailuser
- ``dovecot_auth_pgsql: false`` Use postgresql database for User, not full supported by this role
- ``dovecot_imapd: true`` Enable imap module in dovecot, required for use imap
- ``dovecot_lmtpd: true`` Enable local mail transport in dovecot
- ``dovecot_sieve: false`` Enable serverside filter
- ``dovecot_sieve_default_script: false`` Use default sieve rule files/default.sieve
- ``ufw_imap_public: "{{ dovecot_imapd }}"`` Open TCP 143 in Firewall
- ``ufw_imaps_public: "{{ dovecot_imapd }}"`` Open TCP 993 in Firewall
- ``dovecot_cert_path: "/etc/ssl/letsencrypt/certs/{{ postfix_fqdn }}"`` Path to SSL certs
- ``dovecot_postmaster: "postmaster@{{ dovecot_domain }}"`` Address of Postmaster (Sender address for error messages)

Example Playbook
----------------

    - hosts: servers
      vars:
         - mailuser:
             - domain: "{{ ansible_domain }}"
               users:
                 - username: "test"
                   pass: "{{ mailpw_test_vault }}"
                   UID: 5001
                 - username: "foo"
                   hash: "{{ mailpwhash }}"
                   UID: 5002
      roles:
         - role: pcopfer.dovecot

License
-------

BSD

Author Information
------------------

pcopfer <christian-platz at pcopfer.de>
