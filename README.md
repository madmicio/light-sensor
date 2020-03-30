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
  ```
