ansible_unmount_image
======================

This is an ansible role to perform Actifio unmount images.

Role Variables
--------------

Following variables are accepted/required for this role. 

### Actifio Applinace Related 

| Variable Name    | Description | Required (Y/N) |
|------------------|---|---|
| act_appliance    | Actifio Appliance IP or FQDN. | Y               |
| act_user         | Actifio username. This should be a Actifio user with System Manage priviledges | Y
| act_pass         | Password for the Actifio User | Y
| act_vendorkey    | Vendor key can be obtained by the customer through opening a Support Case with the CSE. | Y
| act_appname 	   | Source Application name of images | N
| act_mount_host   | Mounted Host Name or VM name if you mounted VMware backup image to ESXi host as New VM | Y
| act_image_name   | Image name (Image_XXXXXX) to be unmounted. Default is 'all' which means all images will be unmounted on the mounted host from the source application | N
| act_label        | Label Name of images | N

Example Playbook
----------------

### DB Application Image Example

```
- name: unmount db image
  hosts: "{{ host_group }}"
  become: yes
  become_method: sudo
  roles:
    - { role: ansible_appaware_mount, act_appliance: my-actifio, act_user: ansible, act_pass: mypassword }
  vars:
    act_vendorkey: "{{ contact CSE to get yours }}"
    act_mount_host: "my-dev-server"
    act_appname: "BEAST"
```

### Mounted VM Image Example

```
- name: unmount vm image
  hosts: localhost
  become: yes
  become_method: sudo
  roles:
    - { role: ansible_appaware_mount, act_appliance: my-actifio, act_user: ansible, act_pass: mypassword }
  vars:
    act_vendorkey: "{{ contact CSE to get yours }}"
    act_mount_host: "NewMounteVM"
    act_appname: "SourceVM"
```

License
-------

Copyright 2018 <Kosala Atapattu kosala.atapattu@actifio.com>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
