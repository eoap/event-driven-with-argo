# Redis' Pub/Sub implementations

## Table of Contents
- [Overview](#overview)
- [Modules](#modules)
- [Execution](#Execution)
---

## Overview
This project leverages Redis Pub/Sub and Streams for efficient real-time processing of Earth Observation (EO) data. It consists of two core modules: a Publisher that generates events based on Sentinel-2 satellite imagery and a Subscriber that consumes and processes these events for downstream applications.
By integrating Redis as an event broker, this implementation ensures low-latency, scalable, and reliable communication between components, making it suitable for geospatial analytics, disaster response, and remote sensing applications.

---
## Modules

1. [Publisher](./pub.ipynb): The Publisher module is responsible for generating events from Sentinel-2 EO datasets and pushing them to Redis Streams.
2. [Subscriber](./sub.ipynb): The Subscriber module listens to Redis Streams, processes incoming EO events, and extracts relevant information for further analysis. 
---
## Execution
It is important to execute the [sub.ipynb](./sub.ipynb) Notebook first and then follow the [pub.ipynb](./pub.ipynb) notebooks to publish events. The reasons behind this ordering of execution are, the subscriber must be started first to ensure it is actively listening for events before the publisher begins sending data; otherwise, any messages sent beforehand will be lost, especially in Redis Pub/Sub, which does not store messages. Once the subscriber is running, it continuously reads messages from the Redis stream, allowing the publisher to then send events, which the subscriber will process and acknowledge upon receipt. Therefore please monitor both notebooks until all events are published.