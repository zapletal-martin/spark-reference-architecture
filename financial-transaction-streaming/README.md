H1 Spark Reference Architecture Financial transactions streaming
H1 Summary

This document describes distributed, large data volume stream processing architecture that was used in a real life production financial transaction processing system. The system receives input data from files at defined times and at the same time continuously ingests data from a streaming integration point, processes and transforms the data as a stream, validates them against known records and finally stores the results.

The full paper is attached in a separate document. It describes architecture, technology choices, explanation of system requirements such as data consistency, integrity, performance, fault tolerance or availability and how the selected technologies and their interoperability fulfil the requirements, focusing on Apache Spark. Cluster and resource management required to fulfil some of the requirements as well as to improve cluster utilisation and achieve financial savings are also thoroughly discussed. Finally scenarios where selected technologies and architecture can not be applied due to specific limitations are discussed.

The application receives multiple types of inputs. One are files from other financial institution uploaded at defined times to an integration point and containing a set of transactions. The other one is integration with other systems through Apache Kafka. The records are processed, validated against known data stored in Cassandra database, transformed and finally stored in Cassandra and relevant information sent to integration points with other internal systems. In addition generation of reports and analytics from the stored result data are required. The application has strict requirements for uptime, availability, consistency, data integrity, scalability and cost optimisation while ideally using OS technologies. For those reasons Mesosphere DSOS was chosen for infrastructure automation, cluster and resource management.

TODO: PIC
architecture-diagram.png

The system mostly follows a streaming data platform architecture pattern where all consumers of the data are kept up to date with subscribed topics and with added batch capabilities for specific tasks. 

TODO: PIC
fig:streamingDataPlatform