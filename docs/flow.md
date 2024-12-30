# Integrating Event-Driven Execution with Argo Workflows

## Introduction

This page details the end-to-end integration and execution flow of the water bodies detection system. 

By combining Argo Workflows and Argo Events, the system achieves seamless automation triggered by geospatial data events.

## Integration Architecture

The integration involves three main layers:

* Event Source Layer: Monitors Redis for events simulated by querying the STAC endpoint.
* Event Routing Layer: The Jetstream event bus routes events from the Redis source to the sensor.
* Workflow Execution Layer: Argo Workflows processes geospatial data and detects water bodies.

## End-to-End Execution Flow

### Step 1: Event Generation

Description: Redis acts as an intermediary for event generation. Events are created by querying a STAC API endpoint for geospatial data.

Details:
* Queries can include filters such as specific time ranges or geographic areas.
* Redis publishes events to the stac-events channel.

### Step 2: Event Source Monitoring

Description: The Redis event source listens for new messages on the stac-events channel.

Details:
* When a new event is detected, it forwards it to the Jetstream event bus.
* Events include metadata such as STAC item IDs, collection details, and timestamps.

### Step 3: Event Routing

Description: The Jetstream event bus acts as a high-performance router for events.

Details:
* Ensures reliable delivery to the event sensor.
* Supports scalable handling of multiple concurrent events.

### Step 4: Sensor Activation

Description: The event sensor listens to the Jetstream bus and triggers workflows.

Details:
* Matches events based on defined criteria (e.g., specific STAC item properties).
* Passes event metadata to the triggered workflow as input parameters.

### Step 5: Workflow Execution

Description: The Argo Workflow executes the pipeline to process geospatial data.

Details:

* The workflow includes two templates:
* Calrissian Template: Runs a CWL pipeline to pre-process data.
* Detection Template: Executes the water bodies detection algorithm.
* Outputs include a GeoTiff file with detected water bodies described as a STAC Item, logs, and diagnostic data.

### Step 6: Results Delivery

Description: The workflow stores outputs in a predefined storage location and updates the STAC catalog with results.

Details:

* Results are made accessible via STAC API endpoints.
* Users or downstream applications can retrieve the outputs for analysis.

## Integration Diagram

TODO (Insert a flowchart or diagram illustrating the flow: Redis → Event Source → Jetstream → Event Sensor → Workflow Execution → Result Storage)

## Key Benefits of the Integration

* Automation: Fully automates the data processing pipeline from event generation to result delivery.
* Scalability: Supports high-throughput event handling and parallel workflow execution.
* Modularity: Easy to extend with additional event sources or processing workflows.
* Real-Time Processing: Responds to geospatial data changes in near real-time.

## How to Test the System

1. Simulate Events: Publish STAC query results to the Redis channel manually or via automation.
2. Monitor Workflow Execution: Use the Argo Workflows UI to track pipeline progress.
3. Validate Outputs: Verify that the workflow generates correct water bodies detection results and updates the STAC catalog.

