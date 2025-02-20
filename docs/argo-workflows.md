# Workflow Orchestration with Argo Workflows

## Introduction
[Argo Workflows](https://argoproj.github.io/workflows/) is a Kubernetes-native workflow orchestration tool that excels at automating complex pipelines.

This section explains how Argo Workflows is utilized in this setup to execute the [water bodies](https://github.com/eoap/mastering-app-package) detection algorithm and related preprocessing tasks.

It focuses on the two workflow templates at the core of this system:

## CWL Execution Template

### Water Bodies Detection Template

These templates form the backbone of the processing pipeline, enabling the execution of tasks based on events triggered by [Argo Events](https://argoproj.github.io/events/).

Key Features of Argo Workflows

* Container-Native: Each step of the workflow runs in its own container, ensuring isolation and scalability.
* Declarative Workflows: Defined in YAML, allowing easy customization and version control.
* Scalability: Leverages Kubernetes to run workflows efficiently across distributed resources.
* Integration: Supports external tools like [Calrissian](https://argoproj.github.io/workflows/) for [CWL](https://www.commonwl.org/user_guide/) execution, making it ideal for Earth Observation Application Packages workflows.

## Workflow Templates

This setup uses two primary workflow templates, each designed for specific tasks:

1. CWL Execution Template

This template executes generic CWL workflows using Calrissian, a lightweight CWL runner optimized for Kubernetes.

**Purpose:**

To process general data preparation tasks or execute modular components of the detection pipeline.

2. Water Bodies Detection Template

This template implements the core water bodies detection algorithm. 

It processes geospatial data retrieved from the STAC endpoint and identifies water bodies using the defined logic.

**Purpose:**

To apply the detection algorithm to geospatial datasets, generating actionable results.

## Workflow Execution Flow

1 **Triggered by Events:**
Workflows are initiated when Argo Events detects an event matching the criteria.

2. **Data Preparation:**

The CWL Execution Template runs preprocessing steps, such as data transformation or tiling.

3. **Algorithm Execution:**

The Water Bodies Detection Template processes the prepared data and generates results.

4. **Result Handling:**

Output data, such as `GeoJSON` files, is stored or published for further analysis.

## Why Use Argo Workflows?

* Ease of Use: Declarative `YAML` syntax simplifies workflow definition.
* Extensibility: Easily integrate custom containers and tools like Calrissian.
* Kubernetes-Native: Leverages Kubernetes' orchestration capabilities for resource efficiency.
* Event-Driven Compatibility: Works seamlessly with Argo Events for real-time pipeline automation.