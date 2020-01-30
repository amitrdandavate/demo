# Secure Build Via ISO

## Role Name - provision_vm
Description - This role help to deploy the new virtual machine using CentOS-7-x86_64-DVD-1908.iso file. Post deployment of VM additional configurations are also performed. The deployed VM is then hardened.

## Requirements

1. ansible 2.9.2
      config file = /etc/ansible/ansible.cfg
      configured module search path = [u'/root/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
      ansible python module location = /usr/lib/python2.7/site-packages/ansible
      executable location = /usr/bin/ansible
      python version = 2.7.5 (default, Apr  9 2019, 14:30:50) [GCC 4.8.5 20150623 (Red Hat 4.8.5-36)]

2. Python modules
    pycdlib-1.9.0.tar.gz
    pyvmomi

## Role Variables

The variables are declared in below file - vars/main.yml

All the variables are configurable except the one which refers to the value of another variable. Not recommended to remove sub-variables from the same. 
e.g. cd_ks_iso_path - this contains to reference other variable like customer.prefix

## Dependencies

    Module dependencies listed above in the requirements section.


## Example Playbook

**Sequence of Playbooks to run**
  tasks/main.yml - will run
    - build_dependencies.yml
    - provision_vm.yml
  tasks/post_vm_deploy.yml

e.g. Run sequence
1. Update hosts file
2. Run playbook
```
   ansible-playbook -k -i hosts  deploy.yml --extra-vars "vm_name=mdrrlyh01"
```
   Watch the progress of VM in vSphere Client. Once the VM with OS is deployed run below playbook to run post deploy configurations.
```
   ansible-playbook -k -i deployed_hosts  roles/provision_vm/tasks/post_vm_deploy.yml
```

## License

Cisco Systems

## Author Information

mvp-appliance-engg(mailer list) <mvp-appliance-engg@cisco.com>
