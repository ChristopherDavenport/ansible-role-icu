# International Components for Unicode

[![Build Status](https://travis-ci.org/ChristopherDavenport/ansible-role-icu.svg?branch=master)](https://travis-ci.org/ChristopherDavenport/ansible-role-icu)

Installs Internation Components for Unicode on Remote Servers

Current Supported Operating Systems include RedHat, Centos, Fedora, Debian,
Ubuntu, FreeBSD(although I don't have a testing environment for FreeBSD in
travis if anyone would like to set that up). It also ignore errors on the
includes so assuming your operating system has the requirements listed below
it should work there as well. Would love some testers for Oracle Linux and
Solaris which I believe should both support this build if they have

There is a sub-branch proving the workability of the ansi-modifications in
the ansi-modifications branch. Which you can check out on travis.

All changes made by internal code are reversible via the boolean switches
discussed below, including switching between versions. An avenue of future expansion would be include a variable with state present or absent to show whether this should be installed or will remove all traces of ICU from
the systems. This would likely include a little manipulation but could be
done easily enough.


## Requirements

None, it will make sure all dependencies are installed on supported systems.
Unsupported systems will need to make sure these programs are present.

These are gcc, g++, gmake/make, and tar in whatever form they take on your distro.

## Role Variables

Available variables are listed below, along with default values
(see ```defaults/main.yml```):

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
the code and this is allowed. Looking at all the folks in the Higher Education
Community.

```
icu_ansi_compatibility=False
```

There is a fix for earlier versions(49-53) of icu baked into this build. I highly
reccomend that you leave these fixes in place as they are just a modification
and the ansible build will fail at the check step and you will need to run the
final install step manually.

```
icu_apply_date_fix: True
```

Finally we start by setting the compiling variable to no and if any changes are made then compilation will be done. However if you would like to force
recompilation set this variable to yes and it will recompile every time.
(Note: Compilation is a non-idempotent operation as it first cleans then remakes)

```
icu_recompile: False
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
