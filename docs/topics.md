# Topics

```puml
@startuml

class "acme-sentinel2-stream-source" as StreamSource

struct "acme-sentinel2-stream-source-collected" as StreamSourceCollected {
  +href: URI
  +producer: String
  +subject: URI
}

class "water-bodies-detection-trigger" as WaterBodiesDetectionTrigger

StreamSource -d-> StreamSourceCollected : Write Event
WaterBodiesDetectionTrigger -u-> StreamSourceCollected : Read Event

@enduml
```
