# HomeAssistant-Scenes
Home Assistant Scenes


Input_boolean samples:

change_scene:
  name: Change Scene
  initial: off

bedtime_mode:
  name: Bedtime Mode
  icon: mdi:bed

cinema_mode:
  name: Cinema Mode
  icon: mdi:theater



#Bedtime mode on:

alias: Bedtime Mode On
description: ""
triggers:
  - trigger: state
    entity_id:
      - input_boolean.bedtime_mode
    from: "off"
    to: "on"
conditions: []
actions:
  - action: script.previous_scene
    metadata: {}
    data: {}
  - action: input_boolean.turn_off
    metadata: {}
    data: {}
    target:
      entity_id: input_boolean.change_scene
  - action: input_boolean.turn_off
    metadata: {}
    data: {}
    target:
      entity_id: input_boolean.cinema_mode
  - action: scene.turn_on
    metadata: {}
    data: {}
    target:
      entity_id: scene.bedtime_mode
  - action: input_boolean.turn_on
    metadata: {}
    data: {}
    target:
      entity_id: input_boolean.change_scene
mode: single


#Bedtime mode previous state:

alias: Bedtime Mode Previous State
description: ""
triggers:
  - trigger: state
    entity_id:
      - input_boolean.bedtime_mode
    from: "on"
    to: "off"
conditions:
  - condition: state
    entity_id: input_boolean.change_scene
    state: "on"
actions:
  - action: scene.turn_on
    metadata: {}
    data: {}
    target:
      entity_id: scene.previous
mode: single


#Cinema mode on

alias: Cinema Mode on
description: ""
triggers:
  - trigger: state
    entity_id:
      - input_boolean.cinema_mode
    from: "off"
    to: "on"
conditions: []
actions:
  - action: script.previous_scene
    metadata: {}
    data: {}
  - action: input_boolean.turn_off
    metadata: {}
    data: {}
    target:
      entity_id: input_boolean.change_scene
  - delay:
      hours: 0
      minutes: 0
      seconds: 0.5
  - action: input_boolean.turn_off
    metadata: {}
    data: {}
    target:
      entity_id: input_boolean.bedtime_mode
  - action: scene.turn_on
    metadata: {}
    data: {}
    target:
      entity_id: scene.cinema_mode
  - action: input_boolean.turn_on
    metadata: {}
    data: {}
    target:
      entity_id: input_boolean.change_scene
mode: single


#Cinema mode previous state

alias: Cinema Mode Previous State
description: ""
triggers:
  - trigger: state
    entity_id:
      - input_boolean.cinema_mode
    from: "on"
    to: "off"
conditions:
  - condition: state
    entity_id: input_boolean.change_scene
    state: "on"
actions:
  - action: scene.turn_on
    metadata: {}
    data: {}
    target:
      entity_id: scene.previous
mode: single


#script
script name (script.previous_scene)

sequence:
  - action: scene.create
    metadata: {}
    data:
      scene_id: previous
      snapshot_entities:
        - light.sonoff_100062a5bc
        - switch.sonoff_hall
        - switch.sonoff_lounge
        - switch.sonoff_kitchen
        - light.sonoff_1000dbd502
        - switch.sonoff_10006bce68
        - cover.left_curtain_curtain
        - cover.center_curtain_curtain
        - cover.right_curtain_curtain
alias: Previous Scene
description: ""
