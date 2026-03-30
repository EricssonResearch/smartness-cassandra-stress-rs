# Smartness Cassandra Stress RS

This repo contains Rust code for our client to stress a Cassandra cluster producing our KPI's.
Client create a session for write operations and a session for read operations and save metrics in separate files for each session. Our percentiles are created in three different behaviors: Cumullated, Drained and Windowed.

It also contains python scripts for our load generator (currently working with sinusoidal waves) and to export metrics from Prometheus.

**Paper:** "An Experimental Framework for Studying Non-IID Data in Federated Learning for Network Telemetry"
**Abstract:**
_The increasing complexity of emerging 5G and 6G network environ-
ments has intensified the need for data-driven automation under heterogeneous
and dynamic conditions. Federated Learning (FL) is a promising paradigm in
this context. This paper presents an experimental framework to generate real-
istic Non-Independent and Identically Distributed (Non-IID) datasets through
controlled execution of a distributed service and telemetry collection, aiming to
improve the applicability of FL in network automation. Using Apache Cassan-
dra as a representative cloud-native application, we construct datasets exhibit-
ing temporal and structural heterogeneity. We statistically characterize these
datasets and evaluate their impact on regression models and horizontal fed-
erated learning using a Wide & Deep architecture. Results show that while
horizontal federation improves generalization compared to direct cross-dataset
transfer, its performance degrades under pronounced structural Non-IID condi-
tions, highlighting both its potential and limitations._

Two other repositories make up the entire environment for the experiments.

[Smartness Experiments](https://github.com/EricssonResearch/smartness-experiments), contains notebooks to analyse dataset and code to run the deep model used in our experiment and federated architecture.

[Datasets](https://github.com/EricssonResearch/telemetry_sbrc_2026), contains dataset produced in our experiments.

# Structure

This repository is structure as follows:

### config:
Contains json files with configurations used in our experiments.

### pyscripts:
Contains python scripts used in our experiments:

#### cassandra_loadgen.py
Script to start our load generator.

#### export_metrics.py
Script to export our Prometheus metrics after our experiments run. 

#### smartness_generate_create_table.py and smartness_generate_inserts.py 
Script to generate create table and inserts that we use in our workload files.

### src:
Rust code to generate our client.

### Cargo.lock and Cargo.toml
List of dependencies for our Rust project.

# Badges considered

The authors consider the following badges as part of the evaluation process:

- Artifacts Available (SeloD)
- Artifacts Functional (SeloF)

# Basic information

## Client

It is necessary to install Rust toolchain to build and generate executable for the client. Information for this process can be acessed on the link below:

https://rust-lang.org/learn/get-started/

## Python scripts

- Python 3.12

## System requirements

- Ubuntu 24.04
- 16Gb RAM
- 13th Gen Intel® Core™ i7-13800H × 20
- 250 Gb Disk
- Latest Rust

# Dependencies

- Rust
- Rustup

These dependencies can be installed following the instruction on this link:
https://rust-lang.org/learn/get-started/

To run our python scripts it is necessary to install Python 3.12.

# Installation

To generate our client executable, it is necessary to run the command:

```
cargo build --release
```

# Minimal test

### Client:

After the installation process, the executable can be found on the target/ directory.

To run our client it is necessary to change some of .json files listed on config folder. It is necessary to change the IP used for the tests.

Follow commands used in our experiments:

T100 schema:
```
nohup ./target/release/smartness-cassandra-stress-rs -w smartness-workload-running-time-mt-v3.json > nohup_fixed_client.log 2>&1 &
```

T300 schema:
```
nohup ./target/release/smartness-cassandra-stress-rs -w smartness-workload-running-time-t300-v3.json > nohup_fixed_client.log 2>&1 &
```

T500 schema:
```
nohup ./target/release/smartness-cassandra-stress-rs -w smartness-workload-running-time-intert-v3.json > nohup_fixed_client.log 2>&1 &
```

### Python scripts:

To run our load generator, it is necessary to change the script _cassandra_loadgen.py_ updating lines 31 and 33 to the right path to client executable and .json used to instantiate clients when load generator is running.

Command used to run load generator:

```
nohup python3 pyscripts/cassandra_loadgen.py -v -s 44,30 --logfile clglog.log 660 46 &
```

# LICENSE

This software is under MIT-License. For more information please read LICENSE file.
