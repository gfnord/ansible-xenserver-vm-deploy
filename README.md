# Readme for Xenserver vm deploys

This repo contains Ansible plays that can do automated installs of a template.

## Automated installs on Xenserver

This section contains info about automated installations on Xenserver, using Ansible.

### Predefined VM flavours

`vmtypes.csv` contains settings for different flavours of VM's. It is possible
to override everything (disk size, ram, cpu weight or count etc.), by
supplying the variables on the command line, and the predefined types can be
changed in `vpstypes.csv` if it's a more permanent change.

#### VM configs (vps types)

These predefined VM configs get loaded automatically

- VM-S - 1GB RAM, 25GB disk, 1 CPU, CPU weight: 64
- VM-M - 2GB RAM, 50GB disk, 1 CPU, CPU weight: 256
- VM-L - 4GB RAM, 100GB disk, 1 CPU, CPU weight: 1024
- VM-XL - 8GB RAM, 200GB disk, 1 CPU, CPU weight: 4096
- VM-XXL - 16GB RAM, 500GB disk, 1 CPU, CPU weight: 16384
- VM-XXXL - 32GB RAM, 1TB disk, 1 CPU, CPU weight: 65536

### Static IP adresses

This playbook uses static IP adresses for now, but support for DHCP assigned
addresses is planned.

### Usage

The following variables are required:

- `hostname`
- `vm_name`
- `vps_type`
- `sr_name`
- `vm_template`

The following variables has sane defaults, set by the VPS types CSV
file. But you can change them, if you want to:

- `memory`
- `disksize`
- `cpu_weight`
- `vcpu_count`

The hosts file contains a list of Xenservers. When running the script, you have
to limit the hosts it's being run on, to the one you wish the VPS to run on. If
you have a Xenserver pool, please use the poolmaster.

#### Example

Edit the file *xenserver_vars.yml* and run

`ansible-playbook -i ./hosts xenserver-vm-deploy.yml`

or

`ansible-playbook -i hosts --limit xen01 xenserver-vm-deploy.yml -e
"hostname=vm01 vm_name=vm01 vps_type=VM-S sr_name=ssd_storage
vcpu_count=2 vm_template='Debian9_template'"`
