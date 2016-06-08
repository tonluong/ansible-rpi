# ansible-rpi

Setup Raspberry Pi using Ansible

- Node.js Current v6.2.1
- Node.js LTS v4.4.5

Features

Software | | &nbsp;
 --- | --- | ---
Node.js Current | v6.2.1 | ARMv6
Node.js LTS | v4.4.5 | ATMv6

<br>
## 1. Put inside Roles folder

```
myansible/
		roles/				<-- Put it here
		playbook.yml
		inventory.yml
		...
	
```
```shell
cd myansible/roles/
git clone https://github.com/tonluong/ansible-rpi.git
```  

<br>
## 2. Setup Playbook, Inventory

playbook.yml

```yaml
---
- hosts: pi

  vars:
    - pi_nodejs_current: true

  roles:
    - ansible-rpi
...
```
<br>
inventory.yml

```yaml
[pi]
192.168.9.5		ansible_ssh_user=pi
192.168.9.6		ansible_ssh_user=pi
```
<br>
## 3. Run it
```shell
cd myansible/
ansible-playbook playbook.yml -i inventory.yml
``` 
    
<br>
---

<br>
## Ansbile Variables

Ansible Variables | Ansible Values | Ansible Tags |  | Notes 
--- | --- | --- | --- | --- | ---
 **TTY Console** | | | 
`pi_console_tty1` | `true` | `default`| `console=tty1` 
`pi_console_tty3` | `true` | `quiet`| `console=tty3` 
&nbsp; | | | 
 **GPU Memory** | | | 
`pi_gpumem_128mb` | `true` | | `gpu_mem=128` 
`pi_gpumem_reset` | `true` | `default`| 
&nbsp; | | | 
 **HDMI Boost** | | | 
`pi_hdmiboost-4` | `true` | | `config_hdmi_boost=4` 
&nbsp; | | | 
 **Locale** | | | 
`pi_locale` | `true` | `us` | 
`pi_locale_lang` | `en_US.UTF-8` (default) | | see list at: `/usr/local/share/i18n/SUPPORTED`
`pi_locale_encoding` | <nobr>`UTF-8` (default)</nobr> | | see list at: `/usr/local/share/i18n/SUPPORTED` 
&nbsp; | | | 
**USB** | | | 
`pi_usb_maxcurrent` | `true` | | `max_current_usb=1`
`pi_usb_maxcurrent_reset` | `true` | | 
&nbsp; | | | 
**Node.js** | | | 
`pi_nodejs_current` | `true` | | Node.js Current v6.2.1, ARMv6
`pi_nodejs_lts` | `true` | | Node.js LTS v4.4.5, ARMv6