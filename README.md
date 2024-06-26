# Ansible Playbook to subscribe existing systems to a Satellite 6

This playbook is the universal tool to subscribe existing or new systems to a Satellite server.

The following use cases are covered:
* System is not subscribed at all and needs to registred to a Satellite Server
* System is subscribed to a medival Satellite 5.x system which is not supported anymore since years and needs to be migrated to a recent Satellite 6 server
* System is subscribed to another Satellite 6 and needs to be migrated to another Satellite
* System is subscribed to the Red Hat CDN and needs to be migrated to a Satellite 6 server
* System can be put into a hostgroup and an initial Ansible Play can be triggered to apply the roles defined in the hostgroup 

In the case of CDN or a previous subscription to another Satellite, the systems are unregistred to not have a double usage of subscriptions. However, it does *not* unsubscribe the system from the Satellite 5, in the case of a problem there is an easy backout plan.

# Author and License
- Luc de Louw <luc@delouw.ch>,<ldelouw@redhat.com>
- License: GPLv3
- Provided as is, not supported, use at your own risk

## Contributions
If you want to contribute to this playbook, just clone and send me a pull request, thank you.

# Requirements

The only requirement is to have subscription-manager installed, otherwise there will be a chicken and egg problem. Well, of course you need to have an Ansible Control Node which can be the Satellite itself, which is recommended.

## Usage

First you need to copy the vars.yml.dist to vars.yml and passwd.yml.dist to passwd.yml. The default password for th vaul file passwd.yml is "changeme". 

Set a new password for the passwd.yml using *ansible-vault rekey passwd.yml* 
Edit the passwd.yml and change the Satellite password to what you are actually us in your environment. This can be done with  *ansible-vault edit passwd.yml*

The variables are mostly set in the inventory files, so you can run the playbook for all servers at once. Be aware to first test the proper configuration in a lab environment.

You can set the variables for capsule, which can be the Satellite itself or an actual Capsule, the Satellite the organization name in the vars.yml. The hosts specific vars go to the inventory file

```
ansible-playbook -i inventory -u root -k subscribe_system_to_sat6.yml
```
