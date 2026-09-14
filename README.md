# PEACLab Research

Research conducted as part of the **PEACLab Research Group at Boston University**, focused on understanding resource underutilization in high-performance computing (HPC) systems and exploring methods for smarter resource allocation.

This repository contains experiments on two HPC workload datasets:

- **Fugaku** — used to study underutilization in allocated CPU cores, execution time, and memory.
- **MARCONI100 (M100)** — used for temporal resource-utilization analysis to understand how CPU, memory, and GPU usage change throughout a job's lifetime.

The broader goal of this work is to investigate how HPC schedulers can make better use of allocated resources and support safer job co-location.

---

## Research Motivation

HPC systems typically allocate a fixed amount of resources to a job before execution begins. These resources can include:

- CPU cores
- Memory
- GPUs
- Execution time

However, the amount of resources requested or allocated to a job may be much larger than what the job actually uses.

This creates **resource underutilization**, where expensive computing resources remain allocated but idle.

For example, a job may:

- request significantly more memory than it ever uses,
- receive more CPU cores than necessary,
- have a much larger execution-time allocation than its actual runtime,
- or use CPU, GPU, and memory resources very differently at different points during execution.

Understanding these patterns can help improve resource scheduling, reduce wasted compute capacity, and potentially reduce the energy consumption of large HPC systems.

---

# Fugaku Analysis

[Fugaku](https://www.r-ccs.riken.jp/en/fugaku/about/) is a large-scale supercomputer operated by the **RIKEN Center for Computational Science in Japan**.

Fugaku contains more than **158,000 compute nodes** and is built using Fujitsu A64FX processors. Each compute node contains 48 computational cores and high-bandwidth memory, making the system suitable for extremely large scientific computing workloads.

The Fugaku workload data used in this research was analyzed to understand the difference between the resources allocated to jobs and the resources actually required by those jobs, and prove the underutilization of these jobs.

The analysis focuses on three major resource dimensions:

### CPU Core Utilization

`Fugaku_Cores.ipynb`

### Execution Time

`Fugaku_ExecTime.ipynb`

### Memory Size

`Fugaku_MMSize.ipynb`

## Fugaku Research Goal

---

# MARCONI100 (M100) Analysis

The second part of this research uses workload data from **MARCONI100 (M100)**, a GPU-accelerated HPC system operated by **CINECA in Italy**.

MARCONI100 consisted of **980 compute nodes**, with each node containing:

- 32 IBM POWER9 CPU cores
- 256 GB of memory
- 4 NVIDIA Volta V100 GPUs

The system was designed for large-scale scientific computing and GPU-accelerated workloads.

Unlike the Fugaku analysis, which primarily investigates job-level resource allocation, the M100 analysis focuses on **how resource usage changes over time within individual jobs**.

---

## Temporal Resource Utilization

A job's resource utilization is rarely constant throughout its execution.

For example, a job may:

1. begin with heavy CPU utilization,
2. transition into a GPU-intensive computation phase,
3. experience periods of low activity,
4. and later increase memory consumption.

If the scheduler only considers the maximum resource requirement of the job, resources may remain reserved even during periods where the job is barely using them.

The M100 experiments therefore analyze **temporal CPU, memory, and GPU utilization profiles**.

The long-term goal is to determine whether these utilization patterns can support:

- smarter resource allocation,
- workload characterization,
- peak-utilization prediction,
- temporal modeling,
- and safe co-location of multiple jobs on the same compute resources.

---

## M100 Notebooks

`big_m100_filtering.ipynb`

Preprocesses and filters the MARCONI100 workload data before analysis.

This notebook prepares the dataset for downstream resource-utilization experiments by selecting relevant jobs and resource measurements.

---

`big_m100_analysis2.ipynb`

Performs exploratory analysis of CPU, memory, and GPU utilization across M100 jobs.

The notebook is used to investigate resource-usage patterns and identify differences between allocated resources and actual temporal utilization.

---

`plotly_visualization.ipynb`

Creates interactive visualizations of resource-utilization profiles using Plotly.

These visualizations make it easier to examine how CPU, GPU, and memory utilization change throughout individual job executions.

---

`plotly_pelt_visualization.ipynb`

Explores temporal resource-utilization profiles using **change-point detection**.

The notebook uses the PELT method to identify points where a job's resource behavior changes significantly.

These change points can divide a job into phases such as:

- high utilization,
- moderate utilization,
- low utilization,
- and transitions between different computational behaviors.

This provides a more structured representation of resource usage over time.

---

# Research Direction

The overall research investigates whether HPC resource allocation can move away from purely static resource requests toward more intelligent and adaptive approaches.

Potential applications include:

### Smarter Resource Allocation

Predict the amount of CPU, memory, GPU capacity, or execution time a job is likely to require before it begins.

### Temporal Resource Modeling

Model how resource utilization changes during a job instead of representing the entire job with a single peak value.

### Safe Job Co-location

Identify jobs with complementary resource-utilization patterns that may be able to safely share compute resources.

For example, a CPU-heavy job and a GPU-heavy job may be able to run simultaneously without significantly interfering with one another.

### Reduced Resource Waste

Better predictions and scheduling decisions could reduce idle CPU cores, unused memory, and underutilized GPUs.

---

# Repository Structure

```text
PeacLab-Research/
│
├── Fugaku_Cores.ipynb
├── Fugaku_ExecTime.ipynb
├── Fugaku_MMSize.ipynb
│
├── big_m100_analysis2.ipynb
├── big_m100_filtering.ipynb
├── plotly_visualization.ipynb
├── plotly_pelt_visualization.ipynb
│
└── README.md
