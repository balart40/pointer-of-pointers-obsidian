---
tags:
  - Certification
  - GCP
  - GoogleCloud
---
## The Value of Data

### How data creates value

### Unlocking business value from data

Data
- Unstructured data
- Semi-structure data
- Structured data
#### Structured data

- Highly organized
- Typically stored in a table
- Examples are spreadsheets or database
- Easy to analyze
#### Semi-structured data

- Organized into a hierarchy
- Without full differentiation or order
- Examples: Emails. HTML. JSON, XML
- Doesn't have a formal structure
- Contains tags for easier analysis
#### Unstructured data

- Doesn't have a predefined data model
- Isn't organized in a predefined model
- Text, data files, infra activity

### Data management concepts

#### Database

An organized collection of data stored in tables and accessed electronically from a computer system
- Relational database (RDBMS)
	- A relational database stores and provides access to data points that are related to one another.
	- Row and columns
	- Highly consistent and reliable
	- suited for large amounts of structured data
	- Designed for business data processing
	- Storing online transactional data
- Non relational database (NoSQL)
	- Doesn't use tabular format
	- Follow a flexible data model
	- Ideal for data with changing organization
	- Ideal for applications with diverse data types

google cloud provide 
- Cloud SQL
- Cloud Spanner
For relational DB

for non-relational DB provides Big table

#### Data warehouses (Structured data)

A data warehouse is an enterprise system used for the analysis and reporting of structured and semi-structured data from multiple sources.

BigQuery is offered as a data warehouse for Google Cloud

Bussines data
- Point of sale
- marketing automation
- CRM data

Adhoc analysis and custom reporting
#### Data lakes (Raw data)

A data lake is a repository designed to ingest, store,  explore, process, and analyze any type or volume of raw data,  regardless of the source, like operational systems,  web sources, social media, or the Internet of Things or IoT.

It can store
- Different types of data
- in its original format
- ignoring size limits
- without much pre-processing
- without adding structure

Google cloud for
- Structured data
	- Cloud SQL
	- Cloud Spanner
	- Big query
- Semi Structure data
	- Datastore 
	- bigtable
- unstructured data
	- Cloud storage
### The role of data in digital transformation

#### First party data

First-party data is the proprietary customer datasets that a business collects from customer or audience transactions and interactions.
#### Second party data

Second-party data often describes first-party data from another organization, such as a partner or other business in their supply chain that can be easily deployed to augment a company's internal datasets
#### Third-party data

Finally, there is third-party data,  which are datasets collected and managed by organizations that do not directly interact with an organization's customers or business. 

These datasets might come from government, nonprofit, or academic sources like weather or public demographic data, or from industry specific sources like analysts reports, or industry benchmarking.
#### the value of data chain

- Data genesis
- Data collection
- Data processing
- Data storage
- Data analysis
- Data Activation
#### Data governance

### Google Cloud data management solutions

#### Unstructured data storage

Object storage is a computer data storage architecture that manages data as objects instead of as file storage, which is a file and folder hierarchy, or as block storage, which is chunks of a disc.

These objects are stored in a packaged format that contains the binary form of the actual data and relevant associated metadata such as creation date, author, resource type and permissions and a globally unique identifier.

- No predefined data model
- Organized in a predefined manner
##### Cloud Storage
- Allows customers to store any amount of data and retrieve it as often as needed
- Fully managed scalable service that has a wide variety of uses
###### Standard Storage
- For frequently accessed or hot data
###### Nearline Storage
- Once per month, data backups, long-term media content
###### Coldline Storage
- once every 90 days
###### Archive storage
- Once a year
#### Structured data storage

Relational Databases
- My SQL
- PostgreSQL
- SQL Server
##### Cloud SQL
- Support managed backups
- encrypts customer data
- includes a network firewall
##### Cloud Spanner
- Fully managed
- Mission Critical
- scales horizontally
- SQL RDBMS that uses joins and secondary indexes
- High Availability
- Handles replicas, sharding, and transaction processing
##### Big query
- fully managed data warehouse
- petabytes of data
- Encryption at rest is encryption used to protect data that's stored on a disk, including solid-state drives or backup media
- Can port dataset to vertex AI
#### Semi-Structured data storage
##### Firestore
- Flexible
- Horizontally scalable
- NoSQL cloud database
- Support datatypes: Nested objects, numbers and strings
- automatically scaling
- offline usage
##### Cloud Bigtable
- Google NoAQL big data database service
- Handle massive workloads
- consistent low latency
- high throughput
- For operational applications
- analytical applications
- > 1TB of semi-structured data
- for ML algorithm
#### Choosing the right storage product

**unstructured data**
- Cloud storage: autoclass
**Structure or semi structured**
- Transactional workload
	- SQL
		- CloudSQL
			- Local regional scalability
		- CloudSpanner
			- Scalability
	- NOSQl
		- Firestore
- Analytical workload
	- SQL
		- BigQuery
	- NoSQL
		- Cloud Bigtable
### Making data useful and accessible

#### Business intelligence and insights using looker

Looker is a Google Cloud business intelligence platform designed to help individuals and teams analyze, visualize, and share data.

Looker supports BigQuery, along with more than 60 different SQL databases. Together, BigQuery and Looker provide rich interactive dashboards and reports without compromising performance, scale, security, or data freshness. 

Looker is also 100% web-based, which makes it easy to integrate into existing workflows and share with multiple teams at an organization.
#### Streaming analytics

Streaming analytics is the processing and analyzing of data records continuously instead of in batches
##### Pub/Sub

Ingests hundreds of millions of events per second

##### Dataflow

Unifies streaming and batch data analysis and builds cohesive data pipelines
##### Data Pipeline

A series of actions or stages that ingest raw data from different sources and then move that data to a destination for storage and analysis
#### Pub/sub and data flow

A popular solution for pipeline design is Apache Beam. It's an open source, unified programming model to define and execute data processing pipelines, including ETL, batch, and stream processing. 

Dataflow handles much of the complexity for infrastructure setup and maintenance and is built on Google's infrastructure.

