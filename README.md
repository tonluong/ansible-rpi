# ansible-rpi

Setup Raspberry Pi using Ansible

- Support  Raspian Jessie, Wheezy (limited support)



Software | | &nbsp;
 --- | --- | ---
Node.js Current | v6.2.1 | ARMv6
Node.js LTS | v4.4.5 | ARMv6

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
## Playbook Variables

```yaml
---
- hosts: pi

  vars:
  		- pi_console_tty3: true
  		- pi_quiet: true
  		...
  		
  roles:
  		- ansible-rpi
...
```

<br>

Playbook Variables | Values | Default | &nbsp;  
------------------ | ------ | :-------: | --- 
 **/boot/cmdline.txt** | | | |
`pi_console_tty1` | `true` |  | `console=tty1` 
`pi_console_tty3` | `true` |  | `console=tty3` 
`pi_cursor_off` | `true` |  | `vt.global_cursor_default=0`
`pi_loglevel_2` | `true` |  | `loglevel=2`
`pi_nologo` | `true` |  | `logo.nologo`
`pi_quiet` | `true` |  | `quiet`
&nbsp; | | | 
 **/boot/config.txt** | | | 
`pi_gpumem_128mb` | `true` |  | `gpu_mem=128` 
`pi_gpumem_reset` | `true` |  | 
`pi_usb_maxcurrent` | `true` |  | `max_current_usb=1`
`pi_usb_maxcurrent_reset` | `true` |  |
`pi_hdmiboost-4` | `true` |  | `config_hdmi_boost=4` 
&nbsp; | | | |
**System Config** | | |  
`pi_local_ssh_key` | `true` |  | Add `~/.ssh/id_rsa.pub` to Pi
`pi_locale` | `true` |  | 
&nbsp;&nbsp;&#8735;`pi_locale_lang` |  | <nobr>`en_US.UTF-8`</nobr> | see list at: `/usr/local/share/i18n/SUPPORTED`
&nbsp;&nbsp;&#8735;`pi_locale_encoding` |  | <nobr>`UTF-8`</nobr> | see list at: `/usr/local/share/i18n/SUPPORTED` 
`pi_getty_tty_off` | `true` |  | 
&nbsp;&nbsp;&#8735;`pi_getty_tty_off_item` |  | `1` | `1`, `2`, `3`, ...
&nbsp; | | |
**Software** | | | |
`pi_nodejs_current` | `true` |  | Node.js Current v6.2.1, ARMv6
`pi_nodejs_lts` | `true` |  | Node.js LTS v4.4.5, ARMv6


<br>
## Pi Reference
Raspberry Pi | CPU Chip | | | |
------------ | ---------| --- | --- | --- |
Compute Module, <br>Pi Zero, Pi A+, Pi B+ | BCM2835 | ARMv6 | 32 Bit | Single Core
Pi 2 B | BCM2836 | ARMv7 | 32 Bit | Quad Cores
Pi 3 B | BCM2837 | ARMv8 | 64 Bit | Quad Cores