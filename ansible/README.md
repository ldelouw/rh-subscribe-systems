# Ansible Playbook to subscribe existing systems

This playbook disables Satellite 5 integration of a system and registers the system against Satellite 6. It does *not* unsubscribe the system from the Satellite 5, in the case of a problem there is an easy backout plan.

## Author
- Luc de Louw <luc@delouw.ch>,<ldelouw@redhat.com>
- License: GPLv3


## Usage

You can set the variables for capsule, which can be the Satellite itself or an actual capsule, the organization name and activationkey in the vars.yml file or provide it as extra-vars in the CLI (or Ansible Tower)

i.e.
```
ansible-playbook -i inventory -u root -k subscribe_system_to_sat6.yml --extra-vars "capsule=capsule.example.com activationkey=rhel7-test"
```
