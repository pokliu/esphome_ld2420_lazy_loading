# ESPHOME LD2420 lazy loading external component
The current ESPHOME (v2023.12.9) version only initializes the LD2420 module at startup. If you use an NPN transistor to control the power supply of the LD2420 module, you will find that if ESPHOME does not communicate with the LD2420 normally when it is powered on and initialized, the LD2420 module will be disabled, and it cannot resume normal use even if you call `restart_module`.   

This repository adds an `init_module` button, and the LD2420 module will not be initialized when powered on. The LD2420 module is initialized only when you click the `init_module` button.   

Combined with the automation function of ESPHOME, you can control the power on and off of the LD2420 module to save energy.   

---
Refer to: [External Component](https://esphome.io/components/external_components)

## Locally usage:
- Clone repository to local storage:
``` sh
cd ~/.esphome/external_components
git clone {This repository url} ld2420
```
- Add external components configration in yaml file:
``` yaml
external_components:
  - source: 
      type: local
      path: .esphome/external_components
    components:
      - ld2420
```
- And add init_module button configration in yaml file:
``` yaml
button:
  - platform: ld2420
    ...
    init_module:
      id: ld2420_init
      name: Init Module
```
- If you wanna init ld2420 module on boot up:
``` yaml
esphome:
  name: ...
  friendly_name: ...
  on_boot:
    priority: -100
    then:
      - button.press: ld2420_init
```

Enjoy it.