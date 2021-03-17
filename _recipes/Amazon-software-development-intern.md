---
layout: post
title: "Software Engineer Intern"
date:   2020-08-10 18:13:22 -0600
categories: Software Industry
author: Shubham Sanghavi
tags: AWS Java 
---

May 2020 - August 2020
# Alexa AI, Amazon, Seattle

I interned with the Alexa AI team in Summer, 2020. The times were strange as the world was fighting a pandemic. However, Amazon was kind enough to convert our internships to remote internships providing me with an extremely valuable experience.

## What I did

Designed, developed and deployed a package that publishes relevant fields from multiple data streams to a monitoring service.

- Implemented production level code, with health metrics and alarms, without any prior Java/Junit/AWS experience
- This will enable automation of routing experiments increasing the limit of concurrent alexa routing experiments by 100 times


*See details below*

### Problem

Lets suppose you ask Alexa to play "Frozen". You could have asked for one of the many songs named "Frozen", or the movie "Frozen" or some youtube video titled "Frozen". Given that Alexa's platform is open for anyone to upload their own services, there are generally multiple providers for a specific request. Alexa has developed a machine learning model that ranks the providers.

Everything on the Alexa pipeline optimizes on customer satisfaction. There are two types of customer feedback metrics available for each request:

1. Implicit feedback - ML model that predicts if the customer was not satisfied based on their reaction like asking Alexa to stop.
2. Explicit feedback - For a very small number of requests, Alexa would ask the customer if the response was appropriate.

The only problem? Alexa serves millions of requests per hour. As each service is responsible for a decision, they would require the results aggregated for the requests that were impacted by their decision to improve. The feedback metrics were collected in an ElasticSearch cluster for debugging purposes as it provides strong searching capabilities. I was tasked with implementing a system that would allow effecient aggregation of these metrics.


### Solution  

Many design solutions were presented and discusses with the team. The two major themes of the solutions were:
1. Query the ElasticSearch cluster for the neccessary metrics as and when needed
2. Publish the metrics to a metric store while writing them to ElasticSearch documents

Finally we setteled with the second approach as ElasticSearch is not designed for effecient aggregation but for effecient search. Where as metric stores are heavily optimized for aggregation and additionally allows setting alarms on this metrics which could autmoate experiment dial-up/down.

I implemented a java package which would publish configured fields from the document to metric stores. Customers of this package were different Alexa teams. The package provided customers to select fields from the document that they wanted to publish and a way to configure the destination metric store. Each incoming request would then be filtered for the fields available and published to each customer metric store that requested it. AWS Cloudwatch was the metric store that was used.

### Contribution

First five weeks of the internship were spent in analyzing different solutions and finalizing the design as it involved many stakeholders.

In the next 6 weeks, I managed to implement production level Java code with well-designed classes and appropriate use of design patterns. The code had 90% coverage with extensive use of Mockito. I familiarized myself with multiple AWS services like SQS, SNS, ElasticSearch, AWS Lambda, etc for designing the system. The implementation involved heavy use of CloudWatch service and ways of authenticating multiple CloudWatch clients from a service.

I aquainted myself well with Amazon's internal deployment tools. Necessary alarams and monitors were added to the package and finally it was merged in production. Having acheived this with zero prioir experience with Java, JUnit, AWS, Mockito, Guice, etc. makes me feel very proud.

### Resutls

The implemented package enabled automation of Alexa experiments. Previously, the experiments had to be dialed-up/down by operation engineers using the feedback metrics from a dashboard. Now, service owners could implement experiment control in the Alexa pipeline by querying the feedback metrics directly from Cloudwatch. The automation of experiment increases the limit of concurrent experiments by atleast 100 times.


