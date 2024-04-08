---
tags:
  - GoogleCloud
  - AI
  - GCP
  - Certification
---
## AI and ML Fundamentals

### Introduction and AI and ML defined

### Artificial Intelligence 

The use of technologies to build machines and computers that are able to mimic cognitive functions associated with human intelligence
- Functions such as: 
	- See
	- Understand
	- And respond to spoken or written language

AI is a set of technologies implemented in a system to let it reason, learn, and act to solve a complex problem.
### Machine Learning

It is a subset of AI that enables a machine to learn from data without being explicitly programmed

It relies on various models to
- Analyze large amounts of data
- Learn from the insights
- Make predictions and informed decisions

Training data
Machine learning algorithm
Machine learning model

### How AI and ML differ from data analytics and business intelligence

Business intelligence and Data analytics look into past or historical data

Use data for future decisions

### Problems that ML is suited to solve

- Replacing or simplifying rule base systems
- Automate processes
	- ML is designed to make predictions and repeated decisions at scale
- Understanding unstructured data
- Personalization
### Why ML requires high-quality data

Data is considered low quality if:
- Is not aligned to the problem
- biased in some way

An ML model can't make accurate predictions by learning from incorrect data

Data is evaluated in quality in 6 dimensions:
- Completeness
- Uniqueness
- timeliness
- Validity
- Accuracy
- Consistency 
#### Completeness

The completeness of the data refers to whether all the required information is present
#### unique

Data should be unique
#### Timeliness

The data is up-to-date and reflects the current state of the phenomenon that is being modeled
#### Validity 

The data conforms to a set of predefined standards and definitions such as type and format
- Type
- format
- range
#### Accuracy

Accuracy reflects the correctness of the data
- Form
#### Consistency

Consistency of the data refers to whether the data is uniform and doesn't contain any contradictory information
### The importance of responsible and explainable AI

- Socially beneficial
- avoid creating or reinforcing unfair bias
- be built and tested for safety, 
- be accountable to people, incorporate privacy design principles, 
- uphold high standards of scientific excellence.

## Google cloud AI and ML Solutions

- Big query ML
	- Use SQL queries to create and execute machine learning models in BigQuery
- Pre-trained APIs
	- Leverage ML models that have already been built and trained by google
- Auto ML
	- A no-code solution to build ML models on vertex AI
- Custom training
	- Code your own ML environment to have the control over the ML pipeline
### Big Query ML

Not require Java or Python necessarily 

Compatible with vertex AI model registry
- Can be deployed to endpoints for online prediction
### Pre-trained APIs

- If you do not have your training data
- when you don't have specialized data scientists
- But you have business analysts and developers

Fastest approach but les customizable

APIs can be deployed in 
- VPC
- on-premises
- google public cloud

- Vision API
- Natural Language API
	- discover syntax and sentiment
- Cloud translation API
- Speech-to-text API
- Text-to-speech API
- Video intelligence API
### Auto ML

Train models using your data

Vertex AI brings together Google Cloud services for building ML in a unified UI

Auto ML lets you build ML models with a GUI

for your custom machine-learning models
- example if your text does not fix the entries of Natural Language API
### Custom models

Vertex AI is used for custom End-to-end ML models

Provides a suite of features for each stage of the ML workflow

- Gathering data
- feature engineering
- build model
- deploy and monitor those models

There is no one-size-fits-all all
### Tensor Flow

End to End open source platform for machine learning

TPU - Tensor Processing Unit

Domain Specific Hardware
### AI solutions

Contact Center AI
- Speaking with human agents
Document AI
- Classifying information, receipts, etc
Discovery AI for retail
- ML to select the optimal order of products
Cloud talent Solution
- Matches job candidates faster
### Considerations When selecting Google Cloud AI/ML Solutions

- Speed
	- How quickly Model to production
		- 3 to 36 months
	- Pre-trained API ready to use
	- Custom takes more time, unlike big query ML and autoML
- Differentiation
	- How unique can your model is or need to be
	- Google cloud solution
	- Vertex AI
		- Unified platform for building deploying and managing AI solutions
		- full control
- Expertise required
	- Role: data engineer, data scientist, ML engineers
- Effort required
