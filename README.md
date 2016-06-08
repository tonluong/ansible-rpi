# ansible-rpi

Setup Raspberry Pi using Ansible

Variables | Ansible Values | Tags |  | Notes 
--- | --- | --- | --- | --- | ---
 **Console** | | | 
`pi_console_tty1` | `true` | | `console=tty1` 
`pi_console_tty3` | `true` | | `console=tty3` 
 **GPU Memory** | | | 
`pi_gpumem_128mb` | `true` | | `gpu_mem=128` 
`pi_gpumem_reset` | `true` | | 
 **HDMI Boost** | | | 
`pi_hdmiboost-4` | `true` | | `config_hdmi_boost=4` 
 **Locale** | | | 
`pi_locale` | `true` | | 
`pi_locale_lang` | `en_US.UTF-8` | | see list at: `/usr/local/share/i18n/SUPPORTED`
`pi_locale_encoding` | <nobr>`UTF-8` (default)</nobr> | | see list at: `/usr/local/share/i18n/SUPPORTED` 
**USB** | | | 
`pi_usb_maxcurrent` | `true` | | `max_current_usb=1`
`pi_usb_maxcurrent_reset` | `true` | | 
&nbsp; | | | 
**Node.js Current** | | | 
`pi_nodejs_current` | `true` | | Node.js Current v6.2.1 (ARMv6)
`pi_nodejs_lts` | `true` | | Node.js LTS v4.4.5 (ARMv6)