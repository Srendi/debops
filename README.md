## apparmor

[![Travis CI](http://img.shields.io/travis/ypid/ansible-apparmor.svg?style=flat)](http://travis-ci.org/ypid/ansible-apparmor)
[![Ansible Galaxy](http://img.shields.io/badge/galaxy-ypid.apparmor-660198.svg?style=flat)](https://galaxy.ansible.com/list#/roles/3015)
[![Platforms](http://img.shields.io/badge/platforms-debian-lightgrey.svg?style=flat)](https://galaxy.ansible.com/list#/roles/3015)
[![GitHub Tags](https://img.shields.io/github/tag/ypid/ansible-apparmor.svg)](https://github.com/ypid/ansible-apparmor)
[![GitHub Stars](https://img.shields.io/github/stars/ypid/ansible-apparmor.svg)](https://github.com/ypid/ansible-apparmor)


Configure apparmor.

See [Apparmor in the Debian Wiki](https://wiki.debian.org/AppArmor/HowToUse).

By default (e.g. no [auditd] installed) log messages are logged via syslog to
the kernel facility which usually ends up under /var/log/kern.log.

### Profiles

If some profiles are not quite working, you can checkout the profiles from Debian Stretch or if the problem is specific to your setup, add an exception for example with the [ypid.apparmor_local_config] role.

Here is an example snippet which can be used together with the [debops.apt_preferences] role to get a more recent set of profiles in case you are using Debian Jessie. Note that you have to enable the Stretch sources in APT for this to work.

```YAML
apt_preferences_host_list:
  - package: 'apparmor-profiles'
    raw: |
      Package: apparmor-profiles
      Pin: release o=Debian,n=stretch
      Pin-Priority: 800
```

[auditd]: https://packages.debian.org/search?keywords=auditd
[ypid.apparmor_local_config]: https://galaxy.ansible.com/list#/roles/4649
[debops.apt_preferences]: https://galaxy.ansible.com/list#/roles/1552

### Installation

This role requires at least Ansible `v1.3`. To install it, run:

```Shell
ansible-galaxy install ypid.apparmor
```

To install via git, run either:

```Shell
git clone https://github.com/ypid/ansible-apparmor.git ypid.apparmor
git submodule add https://github.com/ypid/ansible-apparmor.git ypid.apparmor
```


### Role dependencies

- `debops.grub`

### Role variables

List of default variables available in the inventory:

```YAML
---

apparmor_packages:
  - apparmor
  - apparmor-utils
  - apparmor-profiles
  - apparmor-profiles-extra

  # - apparmor-notify
  ## Not needed/useful for servers.

## Default kernel options needed to enable Apparmor.
## You probably don’t need to change this.
apparmor_kernel_options: ['apparmor=1', 'security=apparmor']

## How this role should write the required kernel options into the Grub configuration.
## Default is to use [debops.grub](https://github.com/debops/ansible-grub) as role dependency.
## If set to False, this role will do that internally without debops.grub as role dependency.
## Note that this role is not as flexible in configuring Grub as debops.grub is.
apparmor_manage_grub: False

## Legacy:
## Only considered when `apparmor_manage_grub == True`.
apparmor_additional_kernel_parameters: ''

apparmor_enable: True

## Put all profiles into enforcement mode.
## Use this only if you know what you are doing.
apparmor_enforce_all_profiles: False
```




### Authors and license

`apparmor` role was written by:

- [Robin Schneider](https://github.com/ypid) | [e-mail](mailto:ypid@riseup.net)

License: [AGPLv3](https://tldrlegal.com/license/gnu-affero-general-public-license-v3-%28agpl-3.0%29)

***

README generated by [Ansigenome](https://github.com/nickjj/ansigenome/).
