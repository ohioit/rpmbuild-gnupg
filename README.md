# GnuPG 2.1.x for RHEL6

Some vendors have stopped supporting files encrypted with GnuPG < v2.1. Unfortunately,
The base GnuPG in both RHEL6 & RHEL7 is v2.0 and there are very few alternative sources
for binary installs of GnuPG for RHEL. Compiling GnuPG is not terribly difficult, but
it does involve some dependencies and at least one configure option for older kernels.
Building RPM packages is also not terribly difficult, but updating them and maintaining
them without a centralized build server can be a little problematic. This Vagrant/Ansible
playbook provides a way to reliably update and rebuild a version of GnuPG for RHEL6 which
should not conflict with any of the base system packages.

## Requirements

- Vagrant <https://www.vagrantup.com/>
- VirtualBox <https://www.virtualbox.org/>
- Ansible <https://www.ansible.com/>

## Vagrant/Ansible Usage

```shell
git clone https://github.com/ohioit/vagrant-gnupg.git
cp defaults.yml local.yml
# Modify local.yml as needed, i.e. vendor information
vagrant up
```

If everything works properly you should end up with a freshly cut RPM in the 'out' directory.
You can simply run `vagrant destroy -f` at this point if you like. All you need is the new
RPM file which can be distributed to your servers.

## Custom GnuPG Usage

Once you have installed the RPM on the target system you should be able to use the new version
of GnuPG with something like this:

```shell
source /opt/oit/gnupg/enable
gpg --version
```

You may need change your source path if you changed the vendor information in local.yml.