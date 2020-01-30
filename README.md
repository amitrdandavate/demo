# Secure Build via ISO

## Role Name - provision_vm
Description - This role helps to deploy the new virtual machine using CentOS-7-x86_64-DVD-1908.iso file. Post deployment of VM additional configurations are also performed and the deployed VM is then hardened.

## Requirements

1. Ansible 
```
ansible 2.9.2
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/root/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/site-packages/ansible
  executable location = /usr/bin/ansible
  python version = 2.7.5 (default, Apr  9 2019, 14:30:50) [GCC 4.8.5 20150623 (Red Hat 4.8.5-36)]
```
2. Python modules
```
    pycdlib-1.9.0.tar.gz
    pyvmomi 6.7.1
```
3. Download the hardening rpm [csco-cms-hardening-1.0.0-1.0.noarch.rpm] from artifactory and put inside qs yum repo. [e.g. http://REPOURL/sapphire/]

## Role Variables

The variables are declared in below file - vars/main.yml

All the variables are configurable except the one which refers to the value of another variable. Not recommended to remove sub-variables from the same. 
e.g. cd_ks_iso_path - this contains a reference to other variable like customer.prefix
```
cd_ks_iso_path: "[datastoresas] ISO/{{ customer.prefix }}_kickstart.iso"
```

## Dependencies

Module dependencies listed above in the requirements section.


## Example Playbook

**Sequence of Playbooks to run**
- tasks/main.yml - will run
    - build_dependencies.yml
    - provision_vm.yml
- tasks/post_vm_deploy.yml

e.g. Run sequence
1. Update hosts, deployed_hosts file. 
[ansible_srv] - For Ansible server host
[deployed_host] - For VM to deploy/deployed host

2. Run playbook. When password prompted, provide ansible user password.

```
   e.g.
   $ ansible-playbook -k -i hosts  deploy.yml --extra-vars "vm_name=mdrrlyh01"
   SSH password:
```
   Watch the progress of VM in vSphere Client. Once the VM with OS is deployed run below playbook to run post deploy configurations.
```
   e.g.
   ansible-playbook -k -i deployed_hosts  roles/provision_vm/tasks/post_vm_deploy.yml
   SSH password:
```

## License

Cisco Systems

## Author Information

mvp-appliance-engg(mailer list) <mvp-appliance-engg@cisco.com>
