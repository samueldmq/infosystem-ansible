# InfoSystem Ansible Role

Deploy flask systems based on
[infosystem](https://github.com/samueldmq/infosystem).

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

    ansible servers -m ping -u {username}

### Ansible Hosts

Install ssh:

    sudo apt-get install ssh

Add the ssh public key from the user running the Ansible role in the remote
server to `authorized_keys`:

    ssh-copy-id {username}@{remote server}

Define super user privilegies to the user running the Ansible role in the
remote server by running `sudo visudo` and adding:

    {username} ALL=(ALL) NOPASSWD:ALL

## Role Variables

The following variables are located in `vars/main.yml` and may be configured:

    app_name: the application name, used to name files and processes for this
              role. (defaults to "infosystem")
    app_port: the port the application will be running on.
              (defaults to "5000", the flask's default)
    config_dir: the directory where the application specific configuration will
                be stored. (defaults to "/etc/infosystem")
    wsgi_dir: the directory where the WSGI script will be copied and the Python
              virtual environment will be installed.
              (defaults to "/var/www/infosystem")

## Dependencies

There is no dependency on other Ansible roles.

## Example Playbook

Create a `main.yml` file:

    - hosts: servers
      sudo: yes
      roles:
         - infosystem-ansible

And run it as super user with:

    ansible-playbook -s main.yml

Remember to tell Ansible where this role is located in your filesystem by
editing `roles_path` entry in `/etc/ansible/ansible.cfg`.

## License

Apache-2

## Author Information

Samuel de Medeiros Queiroz: [WebSite](http://www.samueldmq.com),
[GitHub](https://github.com/samueldmq),
[LinkedIn](https://br.linkedin.com/in/samueldmq),
[Email](mailto:samueldmq@gmail.com)