## What is ansible-user?

It is an [ansible](http://www.ansible.com/home) role to create a user and perform common tasks such as transferring a public ssh key and enabling password less sudo for that user.

### What problem does it solve and why is it useful?

Often times you just want a single user created on a box with a few common tasks taken care of for you.

ansible-user solves this by wrapping them together in 1 role so you don't have to worry about the minutia of writing these tasks in every playbook.

## Role variables

```
---
user_name: deploy
user_local_ssh_key_path: ~/.ssh/id_rsa.pub
```

The local ssh key path will be transferred from your workstation to the server(s) being provisioned.

## Example playbook

For the sake of this example let's assume you have a group called **app** and you have a typical `site.yml` file.

To use this role edit your `site.yml` file to look something like this:

```
---
- name: ensure app servers are configured
- hosts: app

  roles:
    - { role: nickjj.user, tags: user }
```

Let's say you want to edit the user name, you can do this by opening or creating `group_vars/app.yml` which is located relative to your `inventory` directory and then making it look something like this:

```
---
user_name: thor
```

## Installation

`$ ansible-galaxy install nickjj.user`

## Requirements

Tested on ubuntu 12.04 LTS but it should work on other versions that are similar.

## Ansible galaxy

You can find it on the official [ansible galaxy](https://galaxy.ansible.com/list#/roles/818) if you want to rate it.

## License

MIT