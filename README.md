# InfoSystem Ansible Role [![Build Status](https://travis-ci.org/samueldmq/infosystem-ansible.svg?branch=master)](https://travis-ci.org/samueldmq/infosystem-ansible)

Deploy flask systems based on
[infosystem](https://github.com/samueldmq/infosystem). The system is downloaded
from its GIT repository and then installed and configured.

## Requirements

No specific pre-requisites other than having [Ansible](https://www.ansible.com)
itself installed and configured.

### Ansible Server

You may install Ansible itself with:

    sudo apt-add-repository -y ppa:ansible/ansible
    sudo apt-get update
    sudo apt-get install -y ansible

Remember to configure the hosts Ansible is able to connect in
`/etc/ansible/hosts` as:

    [servers]
    127.0.0.1

It may be tested by running:

    ansible servers -m ping -u <username> -k

### Ansible Hosts

Install ssh:

    sudo apt-get install ssh

## Role Variables

The following variables are located in `vars/main.yml` and may be configured:

    app_name: the application name, used to name files and processes for this
              role. (defaults to "https://{{ git_user }}:{{ git_passwd }}@github.com/samueldmq/infosystem")
    app_git: the GIT url to download the code from.
              (defaults to "5000", the flask's default)
    app_port: the port the application will be running on.
              (defaults to "5000", the flask's default)
    config_dir: the directory where the application specific configuration will
                be stored. (defaults to "/etc/infosystem")
    force_update: whether the system should be reinstalled. (defaults to true)
    wsgi_dir: the directory where the WSGI script will be copied and the Python
              virtual environment will be installed.
              (defaults to "/var/www/infosystem")

In addition, provide `--extra-vars "git_user=<username> git_passwd=<passwd>"`
in your ansible-playbook call.

## Dependencies

There is no dependency on other Ansible roles.

## Example Playbook

Create a `main.yml` file:

    - hosts: servers
      sudo: yes
      roles:
         - infosystem-ansible

And run it as super user with:

    ansible-playbook -s main.yml -u <username> -k --ask-sudo-pass --extra-vars "git_user=<username> git_passwd=<passwd>"

Add `-e 'ansible_ssh_port=<port>'` to the above command if you need to connect
to a different ssh port of the remote machine.

Remember to tell Ansible where this role is located in your filesystem by
editing `roles_path` entry in `/etc/ansible/ansible.cfg`.

## License

Apache-2

## Author Information

Samuel de Medeiros Queiroz: [WebSite](http://www.samueldmq.com),
[GitHub](https://github.com/samueldmq),
[LinkedIn](https://br.linkedin.com/in/samueldmq),
[Email](mailto:samueldmq@gmail.com)
