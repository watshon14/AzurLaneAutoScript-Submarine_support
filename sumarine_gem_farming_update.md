# Submarine support for gem farming

files to change
edited files are in folder called submarine_gem_farming
and change the deploy.yaml's repository to this repository

# **config/template.json**

                    "StopCondition": {
                    "OilLimit": 1000,
                    "RunCount": 0,
                    "MapAchievement": "non_stop",
                    "StageIncrease": false,
                    "GetNewShip": false,
                    "ReachLevel": 0
                  },
                  "Fleet": {
                    "Fleet1": 1,
                    "Fleet1Formation": "double_line",
                    "Fleet1Mode": "combat_auto",
                    "Fleet1Step": 3,
                    "Fleet2": 2,
                    "Fleet2Formation": "double_line",
                    "Fleet2Mode": "combat_auto",
                    "Fleet2Step": 2,
                    "FleetOrder": "fleet1_all_fleet2_standby"
                  },
                  
```json
                  "Submarine": {
                    "Fleet": 0,
                    "Mode": "do_not_use",
                    "AutoSearchMode": "sub_standby",
                    "DistanceToBoss": "use_open_ocean_support"
                  },
```


                  "Storage": {
                    "Storage": {}
                  }
                },
                "EventGeneral": {
                  "EventGeneral": {
                    "PtLimit": 0,
                    "TimeLimit": "2020-01-01 00:00:00"
                  },
                  "TaskBalancer": {
                    "Enable": false,
                    "CoinLimit": 10000,
                    "TaskCall": "Main"
                  },
                  "Storage": {
                    "Storage": {}
                  }
                },
                "Event": {
                  "Scheduler": {
                    "Enable": false,
                    "NextRun": "2020-01-01 00:00:00",
                    "Command": "Event",


# **module/config/argument/args.json**

      "Fleet2Step": {
        "type": "select",
        "value": 2,
        "option": [
          2,
          3,
          4,
          5
        ]
      },
      "FleetOrder": {
        "type": "select",
        "value": "fleet1_all_fleet2_standby",
        "option": [
          "fleet1_all_fleet2_standby",
          "fleet1_standby_fleet2_all"
        ],
        "display": "display"
      }
    },
```json
    "Submarine": {
      "Fleet": {
        "type": "select",
        "value": 0,
        "option": [
          0,
          1,
          2
        ]
      },
      "Mode": {
        "type": "select",
        "value": "do_not_use",
        "option": [
          "do_not_use",
          "hunt_only"
        ],
        "display": "display"
      },
      "AutoSearchMode": {
        "type": "select",
        "value": "sub_standby",
        "option": [
          "sub_standby",
          "sub_auto_call"
        ],
        "display": "hide"
      },
      "DistanceToBoss": {
        "type": "select",
        "value": "use_open_ocean_support",
        "option": [
          "to_boss_position",
          "1_grid_to_boss",
          "2_grid_to_boss",
          "use_open_ocean_support"
        ],
        "display": "hide"
      }
    },
```

```
    "Storage": {
      "Storage": {
        "type": "storage",
        "value": {},
        "valuetype": "ignore",
        "display": "disabled"
      }
    }
  },
  "EventGeneral": {
    "EventGeneral": {
      "PtLimit": {
        "type": "input",
        "value": 0
      },
      "TimeLimit": {
        "type": "datetime",
        "value": "2020-01-01 00:00:00",
        "validate": "datetime"
      }
    },
```


 
# **module/config/argument/override.yaml**


```
GemsFarming:
  Campaign:
    Event:
      value: campaign_main
    Mode: normal
    UseClearMode: true
    UseFleetLock: true
    Use2xBook: false
    AmbushEvade: true
  StopCondition:
    RunCount: 0
    MapAchievement: non_stop
    StageIncrease: false
    GetNewShip: false
    ReachLevel: 0
  Fleet:
    FleetOrder:
      display: display
      value: fleet1_all_fleet2_standby
      option: [ fleet1_all_fleet2_standby, fleet1_standby_fleet2_all ]
```
  ```json
  Submarine:
    Mode:
      display: display
      value: do_not_use
      option: [ do_not_use, hunt_only ]
    AutoSearchMode: sub_standby
    DistanceToBoss: use_open_ocean_support
```
```
Event:
  Campaign:
    Mode: normal
    Event:
      type: state
    AmbushEvade: true
Event2:
  Campaign:
    Mode: normal
    Event:
      type: state
    AmbushEvade: true
```



 
# **module/config/argument/task.yaml**
    Main3:
      - Scheduler
      - Campaign
      - StopCondition
      - Fleet
      - Submarine
      - Emotion
      - HpControl
      - EnemyPriority
    GemsFarming:
      - Scheduler
      - GemsFarming
      - Campaign
      - StopCondition
      - Fleet
  ```json      
  - Submarine
```
