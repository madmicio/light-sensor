# light-sensor
import the project in tasker
edit the password in activity: mqtt luce



**in Home Assistant**

add sensor:

```yaml
- platform: mqtt
  name: tasker 1
  state_topic: "Livello_luce"
  # value_template: "{{ value_json['luminosita'] }}"
  unit_of_measurement: "lux"
```

  add automation:
 
 ```yaml
  - alias: tema_chiaro
  trigger:
    platform: state
    entity_id: input_select.selezione_tema
    to: 'light'
  action:
    service: frontend.set_theme
    data:
      name: soft_ui
- alias: tema_scuro
  trigger:
    platform: state
    entity_id: input_select.selezione_tema
    to: 'dark'
  action:
    service: frontend.set_theme
    data:
      name: Google Dark Theme
  
- alias: tema_luminosita_chiaro
  trigger:
    platform: numeric_state
    entity_id: sensor.tasker_1
    above: 20
  action:
    - service: input_select.select_option
      data:
        entity_id: input_select.selezione_tema
        option: light
- alias: tema_luminosita_scuro
  trigger:
    platform: numeric_state
    entity_id: sensor.tasker_1
    below: 12
  action:
    - service: input_select.select_option
      data:
        entity_id: input_select.selezione_tema
        option: dark
  ```
  
  input_boolean
  
   ```yaml
  selezione_tema:
  name: Selezione Tema
  options:
    - light
    - dark
    - blu
   ```
   **note**
   I used an input_select to have the possibility to select the theme manually in the ui.
with inpunt_boolean you have the possibility to set more than two themes. if you want to use only two themes instead of input_select you can use an input_boolean

