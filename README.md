# configuration_sudoers.d
This is a repository of my sudoers.d configuration files commonly used
to associate local system user groups (linux) with sudo privileges.

# Description
To better implement 'restrictions', and audit trail, associated to priv
tasks in my environments; I use sudoers.d configuration files. This has
only recently been adopted default with Debian, which has now allowed me
to properly isolate these configurations.

# Dependencies
* Linux
* sudo (Package, and privilege)

# IMPORTANT NOTES:
There is an inherit risk in using MY configurations in your environment.
If you do not properly understand the implications, follow instructions,
or have conflicting configurations - you may be at risk.

## `README.md`
It's not parsed, in a Debian default configuration.

## .git Directory
It's not parsed, in a Debian default configuration.

# Development Dependencies
* sudo (Package, and privilege)

# Contributions
Are welcome.

Due to the nature of these files, and their locations, contributing is
a little non standard. Please (See Here)[Contributing]

# Contributing
Please ensure you have read important notes above.

Parsed files within /etc/sudoers.d should be owned by root:root. In fact
, within a Debian environment; you will receive constant warnings if not
so.

This means edits to such files, and as per best practice; should be
completed using `visudo -f filename`.

It's a good idea to then ensure you are tracking and commiting such
changes as the NON ROOT user - which also depends on having your .git
folder not owned by the root:root user. (Which is okay; it's not parsed)

My general workflow;
Root:
  Create sudoers.d files
  Update sudoers.d files via visudo
General User:
  Track git changes
  Commit git changes

# How To
## Install
TO BE DOCUMENTED..

## Basic Use
My sudoers.d configuration files associate the privilege to a local
system group. This means; configurations will do nothing without
appropriate user added to relative groups (After... their creation).

For example;
My apt configuration has multiple group definitions below. To enable
`apt update`, and `apt upgrade` - the group `aptupdateupgrade_sudoers`
must exist, and the user invoking it must be a member of that group.
(Note: I did originally separate update and upgrade, but one is nearly
useless without the other..)

Before creating your groups; you may want to take a moment to consider
Group, and User ID's. These are often assigend in incrementing order,
from 1000, (Where 1000 is generally allocated to the first user upon
system deploy, if you did so). You might want to consider a numbering
scheme.

This isn't much so a 'best practice', as it is just 'general
housekeeping'. Will endeavour to add further links, relative to this.
However, for now; perhaps consider your 'administrative' groups are in 
the 10000 range.

In the example below, we will use the mock user `mockuser`

Create the local system group, similar to;
`sudo addgroup aptupdateupgrade_sudoers`
or (After ensuring 10000 is not already used)
`sudo addgroup aptupdateupgrade_sudoers --GID 10000`

Then, add the user to the group;
`sudo addgroup mockuser aptupdateupgrade_sudoers`.

Your account, after log out / log in - should then have sufficient
privileges to run functions as part of that sudoers.d definition.

`apt update`, and `apt upgrade`.
