# International Components for Unicode
[![Build Status](https://travis-ci.org/ChristopherDavenport/ansible-role-icu.svg?branch=master)](https://travis-ci.org/ChristopherDavenport/ansible-role-icu)

Installs Internation Components for Unicode on Remote Servers

## Requirements
None, it will make sure all dependencies are installed on supported systems

These are gcc, g++, make, and tar in whatever form they take on your distro.

## Role Variables

Available variables are listed below, along with default values (see ```defaults/main.yml```):

The version of ICU you would like to install. Supports 49-58 currently. Most
current is default.

```
icu_version: 58
```

icu_base is the base location for the install.

```
icu_base: /usr/local/include
```


If you would like to set ICU_HOME variable.

```
set_icu_home: False
```

The icu home variable is by default in a new folder hanging off the icu base
this can be overridden by setting icu_home.

```
icu_home: {{ icu_base }}/icu
```

Finally some people may want some less traditional ansi allowances baked into
the code and this is allowed be

```
icu_ansi_compatibility=False
```


## Dependencies

  - None

## Example Playbook

```
- hosts: appserver
  vars:
    set_icu_home: True
  roles:
    - ChristopherDavenport.icu
```

### License

MIT

### Author Information

This role was created in 2016 by Christopher Davenport.
