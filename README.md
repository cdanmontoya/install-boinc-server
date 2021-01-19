Install BOINC Server
=========

This role deploys a [BOINC server on a Docker](https://github.com/marius311/boinc-server-docker) container in the target host.

Requirements
------------

1. Install Ansible

```console
foo@bar:~$ sudo apt-add-repository ppa:ansible/ansible
foo@bar:~$ sudo apt update
foo@bar:~$ sudo apt install ansible
```
2. Configure the target host. For instance, if the target host is `localhost`, then:

Edit hosts file:
```console
foo@bar:~$ nano /etc/ansible/hosts
```

|/etc/ansible/hosts |
|---|
|<p>localhost<br>...</p>|

Define target host variables:

```console
foo@bar:~$ mkdir /etc/ansible/host_vars
foo@bar:~$ nano /etc/ansible/host_vars/localhost
```

    ansible_connection: local
    ansible_python_interpreter: /usr/bin/python3
    ansible_user: <<user>>
    asible_password: <<pass>>
    ansible_sudo_pass: <<pass>>
    
Edit `ansible.cfg` file:

```console
foo@bar:~$ nano /etc/ansible/ansible.cfg
```

Search the `roles_path` variable and uncomment it:

|/etc/ansible/ansible.cfg |
|---|
|   <p>...<br># additional paths to search for roles in, colon separated<br>roles_path    = /etc/ansible/roles <br>...</p>|

    # additional paths to search for roles in, colon separated
    roles_path    = /etc/ansible/roles
    
Install `geerlingguy.docker` role:

```console
foo@bar:~$ ansible-galaxy install geerlingguy.docker
```

Clone the repo
```console
foo@bar:~$ cd /etc/ansible/roles
foo@bar:~$ git clone https://github.com/cdanmontoya/install-boinc-server.git
```

Role Variables
--------------

* **server_ip:** The role takes into account the current target host IP, but it is automatically detected.
* **github_repo_url:** URL to the github BOINC docker repo.
* **installation_path:** The folder where the github repo will be cloned.

Dependencies
------------

* [geerling.docker](https://galaxy.ansible.com/geerlingguy/docker)

Example Playbook
----------------

After f the requirements

    ---
    - name: test playbook
      hosts: localhost
      connection: local
      become: true
      roles:
        - install-boinc-server

License
-------

BSD

Author Information
------------------
This role was made by [@cdanmontoya](https://github.com/cdanmontoya/) in collaboration with [@valcar95](https://github.com/valcar95/), [@dmrmejiar](https://github.com/dmrmejiar), [@santiago-b9826](https://github.com/santiago-b9826), [@randres-arcila](https://github.com/randres-arcila) and [@jhonatanglorys](https://github.com/jhonatanglorys) as an usefull resource for the [@dannymrock](https://github.com/dannymrock)'s Parallel Programming course at Universidad de Antioquia.
