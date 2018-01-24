## What is ansible-user? [![Build Status](https://secure.travis-ci.org/nickjj/ansible-user.png)](http://travis-ci.org/nickjj/ansible-user)

It is an [Ansible](http://www.ansible.com/home) role to:

- Create user groups
- Create a single user and configure its shell
- Enable passwordless sudo
- Set your public SSH key as an authorized key so you can SSH into your server

## Why would you want to use this role?

When you spin up a new box, you'll often want a user to exist so you can run
whatever apps you need to run as that user, because running things as root is a
bad idea from a security POV.

This role does that, but it also includes a few other user related tasks, such
as what's listed above in the bullets. Having all of these things together in
1 role means less work for you to do!

## Supported platforms

- Ubuntu 16.04 LTS (Xenial)
- Debian 8 (Jessie)
- Debian 9 (Stretch)

## Role variables

```
# Optionally create system wide groups. If empty, users will automatically be
# a part of their user's group, ie. deploy:deploy.
user_groups: []

# The user you want to create.
user_name: "deploy"

# Which shell should you default to? Typically "bash" or "sh".
user_shell: "/bin/bash"

# Do you want to enable using sudo commands without a password?
user_enable_passwordless_sudo: True

# When set, this will copy your local SSH public key from this path to your
# user's authorized keys on your server.
#
# If you don't want this behavior then use an empty string as the value but keep
# in mind you won't be able to log in to your server as your new user with SSH
# keys since you won't be authorized.
user_local_ssh_key_path: "~/.ssh/id_rsa.pub"
```

## Example usage

For the sake of this example let's assume you have a group called **app** and
you have a typical `site.yml` file.

To use this role edit your `site.yml` file to look something like this:

```
---

- name: "Configure app server(s)"
  hosts: "app"
  become: True

  roles:
    - { role: "nickjj.user", tags: "user" }
```

Let's say you want to edit the user name, you can do this by opening or
creating `group_vars/app.yml` which is located relative to your `inventory`
directory and then make it look something like this:

```
---

user_name: "thor"
```

Now you would run `ansible-playbook -i inventory/hosts site.yml -t user`.

## Installation

`$ ansible-galaxy install nickjj.user`

## Ansible Galaxy

You can find it on the official
[Ansible Galaxy](https://galaxy.ansible.com/nickjj/user) if you want to rate it.

## License

MIT
