
# ScyllaDB Documentation



## Table of Contents

1. [Introduction](#introduction)
2. [Key Features](#key-features)
3. [System Requirements](#system-requirements)
4. [Installation using Docker](#installation-using-docker)
5. [Basic Operations](#basic-operations)
    - [Starting ScyllaDB](#starting-scylladb)
    - [CQL Shell](#cql-shell)
    - [CRUD Operations](#crud-operations)
6. [Use Cases](#use-cases)
7. [Additional Resources](#additional-resources)

---

## Introduction

ScyllaDB is a high-performance NoSQL database designed for big data workloads. Built from the ground up for horizontal scalability, ScyllaDB is fully compatible with Apache Cassandra, but offers lower latency and higher throughput thanks to its architecture, which is optimized for modern hardware.

Unlike traditional databases, ScyllaDB can manage large-scale data in real-time across many nodes in a cluster, making it ideal for applications like real-time analytics, IoT, and social media applications.

## Key Features

- **High Performance**: ScyllaDB delivers a significant boost in performance over Apache Cassandra by using a shared-nothing, multithreaded architecture.
- **Scalability**: Easily scale your cluster to handle massive datasets and high request throughput.
- **Fault Tolerance**: Automatic data replication and distribution ensure your data is always available, even in the case of node failures.
- **Fully Compatible with Cassandra**: ScyllaDB supports the Cassandra Query Language (CQL), so existing applications built on Cassandra can migrate seamlessly.
- **Efficient Hardware Utilization**: Leverages modern hardware capabilities like multi-core CPUs, RDMA, and NUMA to achieve optimal performance.
- **Elasticity**: Adding or removing nodes from the cluster is simple and does not impact performance.

## System Requirements

- **Operating System**: Linux (preferred), macOS (development purposes), Windows (via WSL for development)
- **CPU**: Multi-core processor (4 cores or more recommended)
- **Memory**: Minimum 4 GB RAM (8 GB or more recommended)
- **Disk**: SSD recommended for better I/O performance
- **Network**: Gigabit Ethernet (recommended for cluster setups)

## Installation using Docker

ScyllaDB can be quickly installed and run in a Docker container. Using Docker allows for a simple setup without having to worry about complex installation procedures, and it’s an excellent way to get started with ScyllaDB for testing, development, and small-scale production use cases.

### Prerequisites

- **Docker**: Make sure Docker is installed on your machine. You can download it from [Docker's website](https://www.docker.com/get-started).

### Steps for Installation

1. **Pull the ScyllaDB Docker image**:

    The official ScyllaDB Docker image is hosted on Docker Hub. To pull the image, run:

    ```bash
    docker pull scylladb/scylla
    ```

2. **Run the ScyllaDB container**:

    After pulling the image, you can start a ScyllaDB container using the following command:

    ```bash
    docker run --name scylla -d --network host scylladb/scylla
    ```

    - `--name scylla`: Assigns a name to the running container.
    - `-d`: Runs the container in detached mode (in the background).
    - `--network host`: Uses the host network for the container. This can be useful for allowing ScyllaDB to communicate with other nodes in the same network.
  
    The ScyllaDB container will automatically start and listen on the default ports (e.g., 9042 for CQL, 7000 for inter-node communication).

3. **Verify the container is running**:

    You can check if the container is running with:

    ```bash
    docker ps
    ```

    This will show a list of running containers. Ensure that `scylla` is listed and running.

---

## Basic Operations

### Starting ScyllaDB

Once the container is running, ScyllaDB should start automatically. If you need to stop or restart the container, you can use the following Docker commands:

- **Stop the container**:

    ```bash
    docker stop scylla
    ```

- **Start the container**:

    ```bash
    docker start scylla
    ```

### CQL Shell

ScyllaDB uses CQL (Cassandra Query Language) for data manipulation. You can interact with ScyllaDB using the `cqlsh` command-line tool inside the container.

To enter the container and start `cqlsh`, run:

```bash
docker exec -it scylla cqlsh
```

### CRUD Operations

**Create a Keyspace**:

```cql
CREATE KEYSPACE example_keyspace WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 3};
```

**Create a Table**:

```cql
CREATE TABLE users (
    user_id UUID PRIMARY KEY,
    name TEXT,
    email TEXT
);
```

**Insert Data**:

```cql
INSERT INTO users (user_id, name, email) VALUES (uuid(), 'John Doe', 'john@example.com');
```

**Query Data**:

```cql
SELECT * FROM users;
```

**Update Data**:

```cql
UPDATE users SET email = 'john.doe@example.com' WHERE user_id = [some-uuid];
```

**Delete Data**:

```cql
DELETE FROM users WHERE user_id = [some-uuid];
```

---

## Use Cases

- **Real-Time Analytics**: With ScyllaDB’s low-latency and high-throughput capabilities, it’s ideal for real-time analytics.
- **IoT**: ScyllaDB scales easily to handle the massive data requirements of IoT devices.
- **Social Media Applications**: Handle high volumes of user data and activity in real-time.

## Additional Resources

- [ScyllaDB Documentation](https://scylladb.com/docs/)
- [ScyllaDB GitHub Repository](https://github.com/scylladb/scylla)
- [ScyllaDB Tutorials](https://scylladb.com/learn/)
- [Community Forum](https://community.scylladb.com)

---


---


