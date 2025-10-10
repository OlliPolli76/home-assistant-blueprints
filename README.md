# home-assistant-blueprints
„Meine Hue Wall Module Blueprints für Home Assistant

# Dropdown Helfer anlegen:
> [!CAUTION]
> Entität ID =
> input_select.zigbee_action_topic

# Automation anlegen:
alias: Zigbee Dropdown aktualisieren
description: Füllt Helfer "Zigbee Action Topic"
triggers:
  - event: start
    trigger: homeassistant
  - hours: /1
    trigger: time_pattern
actions:
  - target:
      entity_id: input_select.zigbee_action_topic
    data:
      options: |
        {% set devices = states
          | selectattr('entity_id', 'match', '^sensor\.zigbee2mqtt_')
          | map(attribute='attributes.friendly_name')
          | list %}
        {{ devices | select('string') | list }}
    action: input_select.set_options
mode: single
