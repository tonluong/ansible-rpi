# ansible-rpi

Raspberry Pi configuration and application install with ansible

- For Raspian Jessie


Install Variable | Apps | Version | Arch
--- | --- | --- | ---
`pi_nodejs` | Node.js Current | v6.2.1 | ARMv6, ARMv7, ARMv8
`pi_nodejs_lts` | Node.js LTS | v4.4.5 | ARMv6, ARMv7, ARMv8
`pi_golang` | Go | v1.6.2 | ARMv6
`pi_omxplayer` | OMXPlayer | v0.3.7-6c90c75 | 

<br>
## 1. Install

```
myansible/
		roles/				<-- Put it here
		playbook.yml
		inventory.yml
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
    - pi_nodejs: true

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

Playbook Variables | Values | Default | &nbsp;  
------------------ | ------ | :-------: | --- 
 **/boot/cmdline.txt** | | | |
`pi_console_tty_off` | `true` |  | 
`pi_console_tty1` | `true` |  | `console=tty1` 
`pi_console_tty3` | `true` |  | `console=tty3` 
`pi_cursor_off` | `true` |  | `vt.global_cursor_default=0`
`pi_loglevel_2` | `true` |  | `loglevel=2`
`pi_nologo` | `true` |  | `logo.nologo`
`pi_quiet` | `true` |  | `quiet`
`pi_consoleblank_off` | `true` |  | `consoleblank=0` <br>Prevents console from going to sleep
&nbsp; | | | 
 **/boot/config.txt** | | | 
`pi_gpumem_quarter` | `true` |  | `gpu_mem_256=64`<br>`gpu_mem_512=128`<br>`gpu_mem_1024=256` 
`pi_gpumem_half` | `true` |  | `gpu_mem_256=128`<br>`gpu_mem_512=256`<br>`gpu_mem_1024=512` 
**`pi_gpumem`** | `true` |  | `gpu_mem=128` 
&nbsp;&nbsp;&#8735;`pi_gpumem_size` |  | <nobr>`128`</nobr> |
`pi_gpumem_reset` | `true` |  | 
`pi_usb_maxcurrent` | `true` |  | `max_current_usb=1`
`pi_usb_maxcurrent_reset` | `true` |  |
`pi_hdmiboost-4` | `true` |  | `config_hdmi_boost=4` 
&nbsp; | | | |
**System Config** | | |  
`pi_local_ssh_key` | `true` |  | Add `~/.ssh/id_rsa.pub` to Pi
**`pi_locale`** | `true` |  | 
&nbsp;&nbsp;&#8735;`pi_locale_lang` |  | <nobr>`en_US.UTF-8`</nobr> | see list at: `/usr/local/share/i18n/SUPPORTED`
&nbsp;&nbsp;&#8735;`pi_locale_encoding` |  | <nobr>`UTF-8`</nobr> | see list at: `/usr/local/share/i18n/SUPPORTED` 
**`pi_timezone`** | `true` |  | 
&nbsp;&nbsp;&#8735;`pi_timezone_location` |  | `America/Los_Angeles` | 
**`pi_keyboard`** | `true` |  | 
&nbsp;&nbsp;&#8735;`pi_keyboard_model` |  | `pc104` | 
&nbsp;&nbsp;&#8735;`pi_keyboard_layout` |  | `us` | 
**`pi_getty_tty_off`** | `true` |  | 
&nbsp;&nbsp;&#8735;`pi_getty_tty_off_item` |  | `1` | `1`, `2`, `3`, ...
&nbsp; | | |
**Apps** | | | |
`pi_nodejs` | `true` |  | Node.js Current 
`pi_nodejs_lts` | `true` |  | Node.js LTS
`pi_golang` | `true` |  | Go
`pi_omxplayer` | `true` |  | Jessie, Wheezy
`pi_install` | <nobr>`- usbmount`</nobr><br>`- vim` |  | Install list of packages 

```yaml
# pi_install
---
hosts: pi
vars:
	- pi_install:
		- usbmount
		- vim
roles:
	- ansible-rpi
...
```

<br>
## Reference
Cost | Pi | Chip | Arch| Speed | Bit | Core | Mem |Support
---: | --- | ---| --- | ---: | --- | ---: | ---: | :---:
$5 | Pi Zero | BCM2835 | ARMv6 | 1 GHz | 32 | 1 | 512MB |
$20 | Pi A+ | BCM2835 | ARMv6 | 700 MHz | 32 | 1 | 256MB |
$25 | Pi B+ | BCM2835 | ARMv6 | 700 MHz | 32 | 1 | 512MB |
$35 | Pi 2 B | BCM2836 | ARMv7 | 900 MHz | 32 | 4 | 1GB |
$35 | Pi 3 B | BCM2837 | ARMv8 | 1.2 GHz | 64 | 4 | 1GB |

<br>
## Playbooks

Playbook | Notes
--- | ---
[playbook-pi-silentboot.yml](#playbook-pi-silentboot.yml) | Good for mediaplayer or signage use case.

<br>
### playbook-pi-silentboot.yml

```yaml
# pi-playbook-silentboot.yml
---
- hosts: pi

  vars:
  		- pi_console_tty_off: true
  		- pi_cursor_off: true
  		- pi_loglevel_2: true
  		- pi_nologo: true
  		- pi_quiet: true
		
		- pi_gpumem_half: true
  		- pi_usb_maxcurrent: true
  		- pi_hdmiboost-4: true
  		
  		- pi_getty_tty_off: true 
  		
  		- pi_omxplayer: true
  		- pi_nodejs: true
  		
  roles:
  		- ansible-rpi
...
```
