# Event driven processing of Application Packages with Argo Events and Workflows

This module demonstrates an event-driven workflow for detecting [water bodies](https://github.com/eoap/mastering-app-package) in Sentinel-2 satellite imagery using [Argo Events](https://argoproj.github.io/events/), [Argo Workflows](https://argoproj.github.io/workflows/), and [Calrissian](https://argoproj.github.io/workflows/). 

It utilizes a [Redis stream](https://redis.io/docs/latest/develop/data-types/streams/) to trigger workflows that process Sentinel-2 imagery and generate outputs using CWL ([Common Workflow Language](https://www.commonwl.org/user_guide/)).

## What Are Argo Workflows and Argo Events?

### Argo Workflows

Argo Workflows is a Kubernetes-native workflow engine that lets you define and run multi-step processes in the form of Directed Acyclic Graphs ([DAGs](https://en.wikipedia.org/wiki/Directed_acyclic_graph)).

Each "step" in a workflow can be a container or an operation, enabling automation of complex tasks like data processing, [ETL](https://www.snowflake.com/guides/etl-pipeline/) jobs, or ML model training.

### Argo Events

Argo Events is an event-driven automation framework for Kubernetes. It allows workflows and other tasks to be triggered in response to various events, such as webhooks, message queues, or timers.

By connecting event sources (like a Redis stream) to sensors that listen for events, you can trigger automated workflows.

## Overview

The module involves:

* [Event Source](https://argoproj.github.io/argo-events/concepts/event_source/): A Redis stream that holds Sentinel-2 image acquisitions.
* [Sensor](https://argoproj.github.io/argo-events/concepts/sensor/): Listens for events from the Redis stream and triggers a workflow to detect water bodies.
* [Argo Workflows](https://argoproj.github.io/workflows/): Executes a CWL-based workflow using Calrissian to process Sentinel-2 images.
* [Calrissian](https://argoproj.github.io/workflows/): An execution engine for running CWL workflows in Kubernetes, integrated with Argo Workflows.

The webpage of the documentation is https://eoap.github.io/event-driven-with-argo. 

[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC_BY--SA_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)