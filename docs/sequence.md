# Sequence Diagrams

## Deployment

```puml
@startuml

autonumber "<b>[00]"

participant "Event Source" as es
participant "Event Source\nController" as esc
control "Event Source\nDeployment" as esd

participant "Sensor" as sensor
participant "Sensor\nController" as sensorc
control "Sensor\nDeployment" as sensord

activate es
activate esc
activate sensor
activate sensorc

par actions occur asynchronously
  esc -> es : Watch
  esc -> esd ++ : Create
else
  sensorc -> sensor : Watch
  sensorc -> sensord ++ : Create
end

deactivate es
deactivate esc
deactivate esd
deactivate sensor
deactivate sensorc
deactivate sensord

@enduml
```

## Ingestion


```puml
@startuml

autonumber "<b>[00]"

box "Producer Network"
participant "Collector" as publisher
database "Redis" as redis
end box

box "Platform Network" #White
control "Event Source\nDeployment" as esd
control "Sensor\nDeployment" as sensord

queue "Event Bus" as evbus
participant "<$node>\nWorkflow" as container
end box

activate esd
activate sensord

activate publisher
activate redis
activate evbus

par actions occur asynchronously
  publisher -> redis : Add new entries
else
  esd ->o redis : Listen
  esd -> evbus : Write ""acme-sentinel2-stream-source-collected"" Events
else
  sensord ->o evbus : Read Events
  sensord -> container ++ : Trigger
  container -> container : Compute

  alt#LightGreen water bodies detection Success
    container --> redis : Write ""acme-water-bodies-detection-success"" Events
else water bodies detection Failure
    container --> redis : Write ""acme-water-bodies-detection-failure"" Events
end

  destroy container
end

deactivate esd
deactivate sensord
deactivate publisher
deactivate redis
deactivate evbus

@enduml
```
