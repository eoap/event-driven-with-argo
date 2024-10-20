# Event driven processing of Application Packages with Argo Events and Workflows

This project demonstrates an event-driven workflow for detecting water bodies in Sentinel-2 satellite imagery using Argo Events, Argo Workflows, and Calrissian. 

It utilizes a Redis stream to trigger workflows that process Sentinel-2 imagery and generate outputs using CWL (Common Workflow Language).

## What Are Argo Workflows and Argo Events?

### Argo Workflows

Argo Workflows is a Kubernetes-native workflow engine that lets you define and run multi-step processes in the form of Directed Acyclic Graphs (DAGs).

Each "step" in a workflow can be a container or an operation, enabling automation of complex tasks like data processing, ETL jobs, or ML model training.

### Argo Events

Argo Events is an event-driven automation framework for Kubernetes. It allows workflows and other tasks to be triggered in response to various events, such as webhooks, message queues, or timers.

By connecting event sources (like a Redis stream) to sensors that listen for events, you can trigger automated workflows.

## Overview

The project workflow involves:

* Event Source: A Redis stream that triggers workflows when new Sentinel-2 image acquisition events are detected.
* Sensor: Listens for events from the Redis stream and triggers a workflow to detect water bodies.
* Argo Workflow: Executes a CWL-based workflow using Calrissian to process Sentinel-2 images.
* Calrissian: An execution engine for running CWL workflows in Kubernetes, integrated with Argo Workflows.