# Lessons Learned from Building an Event-Driven Geospatial Data Pipeline

## Introduction

This page highlights the technical challenges, design decisions, and key insights gained while developing the event-driven geospatial data pipeline. 

It also includes recommendations for future improvements and practical advice for replicating or extending the setup.

## Key Technical Insights

### Event Source Configuration

Challenge: Configuring [Redis](https://redis.io/docs/latest/develop/data-types/streams/) as a reliable event source for [Argo Events](https://argoproj.github.io/events/).

Insight:
* Redis' Pub/Sub feature proved effective but required careful setup to ensure scalability.
* The use of clear naming conventions for Redis channels (e.g., stac-events) simplified debugging.

### Jetstream Event Bus

Challenge: Ensuring reliable and performant event routing.

Insight:
* [Jetstream](https://argoproj.github.io/argo-events/eventbus/jetstream/)’s integration with Argo Events offers a robust event-driven architecture.
* It is crucial to define clear message schemas for event payloads to maintain consistency.


### Workflow Scalability

Challenge: Managing workflows triggered by multiple simultaneous events.

Insight:
* [Argo Workflows](https://argoproj.github.io/workflows/) scales effectively but requires resource limits and quotas to prevent cluster overload.
* Using parameterized templates enabled workflows to process diverse input data dynamically.

## Design Decisions

### Separation of Concerns

Decision: Use Argo Events exclusively for orchestration and delegate processing to workflows.

Outcome:
* Simplified troubleshooting by isolating event-handling logic from data processing logic.

### Modular Workflow Templates

Decision: Separate the [CWL](https://www.commonwl.org/user_guide/) execution and water bodies detection into distinct workflow templates.

Outcome:
* Enhanced reusability for other geospatial pipelines requiring similar preprocessing steps.

### STAC Integration

Decision: Leverage the STAC API for querying and storing geospatial data.

Outcome:
* Improved interoperability with other geospatial tools and standards.

## Challenges and Solutions

### Handling Event Storms

Challenge: Preventing resource exhaustion during high-frequency event generation.

Solution:
* Introduced rate-limiting on the Redis event source and implemented a backoff mechanism.

### Debugging Workflow Failures

Challenge: Diagnosing failures in complex workflows with multiple steps.

Solution:
* Enabled Argo Workflows’ artifact repository to store intermediate outputs and logs for analysis.

### Maintaining Consistency in Results

Challenge: Ensuring consistent outputs across diverse input datasets.

Solution:
* Developed unit tests for the CWL pipeline and water bodies detection algorithm.
* Validated results against a benchmark dataset during development.

## Conclusion

Using Kubernetes-native tools like Argo Workflows and Argo Events, this setup demonstrates how to create a real-time processing system that aligns with modern cloud-native practices.
