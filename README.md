# Smartness Cassandra Stress RS

This repo contains Rust code for our client to stress a Cassandra cluster producing our KPI's.
Client create a session for write operations and a session for read operations and save metrics in a separate files for each session.
Our percentiles are created in three different behaviors: Cumullated, Drained and Windowed.

It also contains python scripts for our load generator (currently working with sinusoidal waves) and to export metrics from Prometheus.

All these tools was developed to produce our paper: "An Experimental Framework for Studying Non-IID Data in Federated Learning for Network Telemetry"
