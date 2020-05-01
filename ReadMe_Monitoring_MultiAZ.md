
# What are some tools for Monitoring infrastructure?

In AWS the tool used for monitoring is Amazon CloudWatch. It is a monitoring and observability service built for DevOps engineers, developers, SREs, and IT managers CloudWatch provides you with data and actionable insights to monitor your applications, respond to system-wide performance changes, optimise resource utilisation, and get a unified view operational health.

CloudWatch collects monitoring and operational data in the form of logs, metrics, and events, providing you with a unified view of AWS resources, applications, and services that run on AWS and on-premises servers. You can use CloudWatch to detect anomalous behaviour in your environments, set alarms, visualise logs and metrics side by side, take automated actions troubleshoot issues, and discover insights to keep your applications running smoothly.

# ELK stack - What it is, and how does it work?

ELK stack is an acronym for Elasticsearch, Logstash, and Kibana. It give you the ability to aggregate logs from all you systems and applications, analyse these logs, and create visualisations for application and infrastructure monitoring.

**E = Elasticsearch**
Elasticsearch is an open-source, RESTful, distributed search and analytics engine built on Apache Lucene. Support for various languages, high performance, and schema-free JSON documents makes Elasticsearch an ideal choice for various log analytics and search use cases.
**L = Logstash**
Logstash is an open-source data ingestion tool that allows you to collect data from a variety of sources, transform it, and send it to your desired destination. With pre-built filters and support for over 200 plugins, Logstash allows users to easily ingest data regardless of the data source or type.

**K = Kibana**
Kibana is an open-source data visualisation and exploration tool for reviewing logs and events. Kibana offers easy-to-use, interactive charts, pre-built aggregations and filters, and geospatial support and making it the preferred choice for visualising data stored in Elasticsearch.

#High Availability - Multi AZ

In Multi-AZ deployment, Amazon RDS provides high availability and durability for DB instances, making them a natural fit for production database workloads. When you provision a Multi-AZ DB instance, Amazon RDS creates a primary DB instance, and synchronously replicates the data to standby instance in a different  AZ (Availability Zone). Each AZ runs its own physically distinct, independent infrastructure and it is highly reliable.

## What are Availability Zones?

With Amazon Web Services data centres have facilities are in different physical locations. The locations are categorised as regions and availability zone.

Each AWS Region is large and widely dispersed into different geographic locations. Hence There are availability zones which exist. These locations are separated that way if one availability zone fails you are able to access the other one within the region. That way your server is always available.

![ElastiCache-RegionsAndAZs](https://user-images.githubusercontent.com/60632288/80703070-033c2b80-8ada-11ea-89fc-c2c75223c37c.png)


## How do you set up a multi Availability zone infrastructure

Using the AWS Management Console, you can easily create new Multi-AZ deployments or modify existing Single-AZ instances to become Multi-AZ deployments.

* To create a new Multi-AZ deployment using the AWS Management Console, simply click the "Yes" option for "Multi-AZ Deployment" when launching a DB Instance.

* To convert an existing Single-AZ DB Instance to a Multi-AZ deployment, use the "Modify" option corresponding to your DB Instance in the AWS Management Console.

# **Sources**
- https://aws.amazon.com/cloudwatch/
- https://aws.amazon.com/elasticsearch-service/the-elk-stack/
- https://www.elastic.co/webinars/elk-stack-devops-environment
- https://aws.amazon.com/rds/features/multi-az/
https://aws.amazon.com/rds/aurora/

#### Author
**Victor Sibanda** - *Junior DevOps Engineer* - [victorsibanda](https://github.com/victorsibanda)
