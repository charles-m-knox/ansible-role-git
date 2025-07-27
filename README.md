# Git

Ansible role that installs and configures git and git lfs.

## Requirements

There are no requirements for this, it should work out of the box with Ansible.

## Role Variables

Please see `defaults/main.yml` for variables that can all be set on a per-host
basis.

In particular, you'll want to set `install_git: true` on your desired hosts, and
then set `git_config_extra_options` to something like this:

```yaml
git_config_extra_options:
  - ["user.name", "example-git-username"]
  - ["user.email", "code@example.com"]
  - ["user.signingkey", "1234567890123456"]
```

You'll also want to review `git_config_common_options` from `defaults/main.yml`,
as these values get set as well.

## Dependencies

None at the moment.

## Usage

First, create a `requirements.yml` in your Ansible setup if you haven't already,
here's an example:

```yaml
---
collections:
  - name: community.general
  - name: ansible.posix
  - name: community.crypto

roles:
  - name: charles-m-knox.git
    src: https://github.com/charles-m-knox/ansible-role-git.git
    scm: git
    version: main
```

Next, install it:

```bash
# include the -f flag to forceably re-install and get the latest (equivalent to
# upgrading)
ansible-galaxy role install -f -r requirements.yml
```

Now, in your `site.yml` (or whatever your playbook is named), use the role -
note that root access is required for some of the steps:

```yaml
- name: git
  hosts: all
  roles:
    - charles-m-knox.git
```

```bash
ansible-playbook site.yml --tags git
```

## License

MIT

## Author Information

<https://charlesmknox.com>
