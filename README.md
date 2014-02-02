# NixOS Vagrant Plugin

This plugin makes working with [NixOS](http://nixos.org) guests much easier to work with in [Vagrant](http://www.vagrantup.com):

* Allow network configurations from Vagrantfile (Vagrant does not have a default NixOS guest capability)
* Allow hostname setting
* Provide a convention for nix provisioning

## Usage:

```bash
$ vagrant plugin install vagrant-nixos
...
```

## How it works

In nixos we don't mess around with the files in `/etc` instead we write delarative expressions for the system configuration starting in `/etc/nixos/configuration.nix`.

This plugin sets some ground rules for nixos boxes to keep this configuration clean.

Box creators should ensure that their `configuration.nix` file imports an empty file `/etc/nixos/vagrant.nix` which will be overwritten by `vagrant-nixos` during `vagrant up` or `vagrant provision` and a `nixos-rebuild switch` will be triggerd.

See the configuration in our [NixOS packer template](http://github.com/oxdi/nixos) for an example.

## Issues

It's a bit slow to boot at the moment as it must run nixos-rebuild several times. This is far from ideal I'm sure I'll find a better place to hook in the rebuild step soon.

