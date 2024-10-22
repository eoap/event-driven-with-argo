# Architecture

```puml
@startuml
!include <kubernetes/k8s-sprites-unlabeled-25pct>

component "Collector" as publisher

database "Redis" as redis

publisher -r-> redis : Add new entries

artifact "Event Source" as es
component "Event Source\nController" as esc
control "Event Source\nDeployment" as esd

esc -u-> es : Watch
esc -d-> esd : Create
esd -l-> redis : Listen

artifact "Sensor" as sensor
component "Sensor\nController" as sensorc
control "Sensor\nDeployment" as sensord
component "<$node>\nWorkflow" as container

sensorc -u-> sensor : Watch
sensorc -d-> sensord : Create
sensord -r-> container : Trigger

queue "Event Bus" as evbus

esd -d-> evbus : Write\nEvents
evbus -u-> sensord : Read\nEvents

@enduml
```