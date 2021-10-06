# Rocket.Chat

Real-time conversations with your colleagues, other companies or customers.<br>
Rocket.Chat does everything other platforms do, except exposing your data.

[Documentation](https://docs.rocket.chat/installing-and-updating/manual-installation/ubuntu)

## Requirements

* Ubuntu Server 20.04
* Ansible 2.9.6

## Initial settings

Define the variables on `inventory.yml` as per your needs

Change variables on `inventory.yml`
```bash
ansible_host: '<hostname>'
username: '<username>'
domain_name: '<domain-name>'
```

Ansible connection can be set as `local` or `ssh`
```bash
ansible_connection: '<connection>'
```

SSH private key file needs to be defined when using `ssh` connection
```bash
ansible_ssh_private_key_file: /path/to/your/ssh-key
```

Install `ansible` in your system
```bash
sudo apt -y install ansible
```
> ansible version 2.9.6

## Setup ssh config

Change ssh-key permissions
```bash
chmod 400 ~/.ssh/<ssh-key>
```

Configure ssh config file
```bash
touch ~/.ssh/config
chmod 600 ~/.ssh/config
```

SSH config file sample
```bash
Host alias
  HostName <ip-address>
  User <username>
  Port 22
  IdentityFile ~/.ssh/<ssh-key>
```

## Usage and information

Install rocketchat on ubuntu server 20.04, add **flag** `-K` in case the user has a password
```bash
ansible-playbook -i inventory.yml rocketchat.yml
```

> Access rocketchat [localhost:3000](http://localhost:3000) or hostname:3000<br>
> It may take a few seconds or minutes to load

### Tags

Using tags helps to define which roles will be selected or skipped

Run only tags with tags `node` and `rocketchat`
```bash
ansible-playbook -i inventory.yml rocketchat.yml --tags "node,rocketchat"
```

Run all tasks except those with the tags `common` and `mongodb`
```bash
ansible-playbook -i inventory.yml rocketchat.yml --skip-tags "common,mongodb"
```

## License

[MIT license](http://opensource.org/licenses/MIT)
