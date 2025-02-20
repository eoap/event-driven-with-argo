# Event-Driven Water Bodies Detection Using Argo Workflows and Argo Events


## Introduction

This learning resource demonstrates an event-driven system for detecting [water bodies](https://github.com/eoap/mastering-app-package) using cloud-native technologies. The system leverages [Argo Events](https://argoproj.github.io/events/) to handle and react to external event sources and Argo Workflows to execute data processing pipelines, including a water bodies detection algorithm encoded in the Common Workflow Language ([CWL](https://www.commonwl.org/user_guide/)).

The workflow is triggered by events simulated through [Redis](https://redis.io/docs/latest/develop/data-types/streams/), an external event source, which queries a SpatioTemporal Asset Catalog (STAC) endpoint. The STAC endpoint provides geospatial data, which serves as the input for the detection algorithm. The automation is achieved using Kubernetes-native tools, making the setup scalable, modular, and suitable for Earth observation and geospatial applications.
This project demonstrates an event-driven workflow for detecting water bodies in Sentinel-2 satellite imagery using Argo Events, Argo Workflows, and Calrissian](https://argoproj.github.io/workflows/). 

It utilizes a Redis stream to trigger workflows that process Sentinel-2 imagery and generate outputs using CWL (Common Workflow Language).


## Key Components

This setup integrates the following technologies and concepts:

### Argo Workflows

* Automates the execution of tasks using predefined workflow templates.
* Supports the execution of CWL workflows using Calrissian, a lightweight executor for CWL in Kubernetes.
* Includes two templates:
  * CWL Execution Template: Executes general CWL workflows, such as preprocessing tasks.
  * Water Bodies Detection Template: Encodes the algorithm for detecting water bodies in geospatial data.

### Argo Events

* Provides an event-driven architecture for triggering workflows.
* Uses a [Jetstream](https://argoproj.github.io/argo-events/eventbus/jetstream/) Event Bus to handle event communication.
* Includes:
  * Redis Event Source: Queries the STAC endpoint to generate simulated events.
  * Event Sensor: Listens for Redis events and triggers the water bodies detection workflow.

### Redis as an Event Source

* Simulates events by querying the STAC endpoint.
* Acts as a lightweight, flexible mechanism to mimic real-time event streams.
* Ensures seamless integration with Argo Events via an event source configuration.

### STAC Endpoint

* Serves as the primary data source, providing geospatial data in a standardized format.
* Enables the workflow to focus on processing relevant datasets for water bodies detection.

## High-Level Architecture

The system is designed to handle the following flow:

1. Event Generation:

* Redis queries the STAC endpoint and generates events containing metadata about geospatial assets (e.g., imagery of specific regions).

2. Event Propagation:

* The Redis Event Source forwards events to the Jetstream Event Bus.

3. Event Sensing and Workflow Triggering:

* The Event Sensor monitors the Jetstream Event Bus for relevant events.
* Upon detecting an event, the sensor triggers the execution of the water bodies detection workflow.

4. Workflow Execution:

* The Argo Workflow templates process the event's input data using the CWL-based algorithm.
* The water bodies detection results are stored or published for further use.

## Why Use This Setup?

This setup showcases the power of combining event-driven paradigms with container-native workflows for scalable geospatial analysis. 

It is particularly suited for Earth observation and scientific workflows because:

* Scalability: Kubernetes ensures workflows can handle varying loads effectively.
* Modularity: Components can be easily reused or replaced for other applications.
* Automation: Events trigger workflows without manual intervention, enabling real-time processing.

Through this resource, you'll learn to implement a cloud-native pipeline for water bodies detection, which can be extended to other geospatial or scientific applications.

