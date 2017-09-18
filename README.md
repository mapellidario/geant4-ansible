# geant4-ansible
Ansible playbook for installing geant4

## Run

Edit the `inventory/group_vars/local.yml` file and set the host machine user and
the versions of `root-cern`, `clhep` and `geant4`. Put `geant4_option_clhep: ""` if
your installation of geant4 does not require the clhep libraries.

Run from this repo directory the following commands:

    ansible-playbook -i inventory/hosts.yml 01-root-cern.yml --ask-sudo-pass -vvvv
    ansible-playbook -i inventory/hosts.yml 02-clhep.yml --ask-sudo-pass -vvvv
    ansible-playbook -i inventory/hosts.yml 03-geant4.yml --ask-sudo-pass -vvvv

or, if you do not need the clhep, only

    ansible-playbook -i inventory/hosts.yml 01-root-cern.yml --ask-sudo-pass -vvvv
    ansible-playbook -i inventory/hosts.yml 03-geant4.yml --ask-sudo-pass -vvvv

## Details

This playbook build locally `root-cern`, `clhep` and `geant4` with `cmake` and
`make`. It creates both build and install directories, so that after the
compilation the source and build directories can be deleted.
The install directories can be found in `~/software`.

Since the playbook is set to use `/bin/bash` for configuring and compiling,
the librearies are all sourced into `~/.bashrc`. If you use a different shell
I guess that you know how to source these libraries based on the
`*_load_command` contained in `inventory/group_vars/local.yml`.

At the end of the playbook the basic B1 example of geant4 is compiled, in
order to test that everything properly works.

## Troubleshoot

I tested these playbooks on a debian machine, the required packages for geant4
and clhep have not even been searched for centos7. Any help in this regard is
pretty much appreciated!

## Further improvements

The `inventory/group_vars/local.yml` file and the geant4 cmake options are a
a mess, they will be tidied up some day.

## Pull Requests

As already mentioned, pull requests are appreciated!
