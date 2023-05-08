# Detection Engineering Pocket Guide

## Table Of Contents

[Definitions](#definitions)

[Methodology](#methodology)

[Visibility](#visibility)

+ [Domain](#domain)
+ [Collection](#collection)
+ [Permanence](#permanence)

[Detection Methods](#detection-methods)

[Alerting Strategies](#alerting-strategies)

+ [Direct Alerting](#direct-alerting)
+ [Signal-Based Alerting](#signal-based-alerting)
+ [Risk-Based Alerting](#risk-based-alerting)

[Detection Systems](#detection-systems)

+ [Data Collection & Storage](#data-collection--storage)
+ [Data Transformation](#data-transformation)
+ [Data Analytics](#data-analytics)
+ [Monitoring & Metrics](#monitoring--metrics)

[Detection Metrics](#detection-metrics)

+ [Coverage](#coverage)
+ [Reliability](#reliability)
+ [Timeliness](#timeliness)

[Relationship to Other Domains](#relationship-to-other-domains)

## Definitions

> ... the design, development, testing, and maintenance of threat detection logic.

+ [Panther](https://panther.com/cyber-explained/detection-engineering-benefits/), 2022

> ... the working end of threat intelligence ... take the intelligence team's threat profiles and prioritization as input with which to build the software and/or analytics that the team will use to detect those threats.

+ [Red Canary](https://redcanary.com/blog/modern-security-operations-center/), 2020

> ... design and build security systems that constantly evolve to defend against current threats.

+ [Gigamon](https://blog.gigamon.com/2020/02/24/so-you-want-to-be-a-detection-engineer/), 2020

## Methodology

Detection engineering should follow the [OODA loop](https://en.wikipedia.org/wiki/OODA_loop):

+ Observe: adversaries in the wild, threat intelligence reports, security advisories
+ Orient: assess applicability to the organization, systems, and data
+ Decide: prioritize detection based on potential risk and available tools
+ Act: develop, test, and deploy detection logic

## Visibility

Visibility describes the availability and applicability of data used in detection engineering. There is no detection engineering without sufficient visibility.

### Domain

Categorizations of data that are available to and can be applied during detection engineering.

#### Host

Contains data that describes traits of and actions taken on an host.<br>
<br>
Examples: process execution, files on-disk, service modification

#### File

Contains data that describes traits of and actions taken by a file.<br>
<br>
Examples: embedded files, static analysis, dynamic analysis

#### Network

Contains data that describes traits of and actions taken on a network.<br>
<br>
Examples: flow records, proxy connections, email messages

#### Cloud

Contains data that describes traits of and actions taken in a cloud service.<br>
<br>
Examples: CloudTrail (AWS), Cloud Audit (GCP), Log Analytics (Azure)

#### Application

Contains data that describes traits of and actions taken by an application.<br>
<br>
Examples: database transactions, online office software

### Collection

Methods used by tools to collect data from a source. Collection methods directly impact the availability of data that is used during detection engineering.

#### Continuous

Data is collected continuously from a source.

#### Scheduled

Data is collected from a source on a schedule (e.g., once per minute, once per hour, etc).

#### Ad Hoc

Data is collected from a source as needed.<br>
<br>
This is rarely useful for proactive threat detection and is better suited for reactive threat assessments.

### Permanence

Lifespan of data as determined or observed by the source. Permanence directly impacts the reliability of data that is used during detection engineering.<br>
<br>
Permanence can be improved through data engineering.

#### Ephemeral

Data that is available for a brief moment of time, usually on the scale of milliseconds to seconds. Ephemeral data represents the highest risk to loss of visibility because the data is irrecoverable.<br>
<br>
Examples: network packets, executed processes

#### Short-Lived

Data that is available for short periods of time, usually on the scale of minutes to hours.<br>
<br>
Examples: packet capture, files on-disk

#### Long-Lived

Data that is available for long periods of time, usually on the scale of days to months.<br>
<br>
Examples: flow records, data backups

## Detection Methods

Methods used to implement detection logic. These methods can be combined to create high complexity logic.

### Match

Triggers detection by alerting on a series of string or regular expression matches.<br>
<br>
Example: fieldX == "foo" and fieldY == /bar$/

### Aggregate

Triggers detection by alerting when a variable exceeds a threshold according to an aggregation function. The most common aggregation is a count that exceeds a static threshold, but more complex aggregations may use statistical functions such as min, max, and standard deviation.<br>
<br>
Example: "foo" appeared more than 10 times over a period of 30 seconds

### Join

Triggers detection by alerting when activities of interest coalesce on a variable across multiple events.

Example: fieldX == "foo" in eventA AND fieldX == "bar" in eventB ON fieldY over a period of 1 minute

## Alerting Strategies

Strategies for applying detection methods to generate alerts.

### Direct Alerting

Alerts are generated directly from a detection method.

### Signal-Based Alerting

Alerts are generated from one or more detection signals, which are atomic behaviors of interest. Signals are aggregated, chained, or joined to create alerts.

### Risk-Based Alerting

Alerts are generated from multiple detection methods that are combined into a risk score. Risk scores are calculated based on the potential impact of a security event or incident.

## Detection Systems

Capabilities provided by detection systems that allow engineers to achieve visibility, apply detection methods, and implement alerting strategies. Systems may provide one, some, or all of these capabilities. All of these capabilities are required to create a "detection platform."

Generally, this is true:

+ The number of capabilities provided by a single tool or service is inversely proportional to the flexibility of the tool or service.
+ The number of tools or services used in a detection platform is directly proportional to the complexity of the platform.

### Data Collection & Storage

Provides the ability to collect and store data from a system or service.

Key considerations:

+ Data collection
  + Which data is necessary to enable detection and response?
  + How is data collected and measured for reliability?
+ Data storage
  + Which data provides short-term and long-term value?
  + What is the cost of storing and retrieving data?

### Data Transformation

Provides the ability to format, normalize, and decorate data.

Key considerations:

+ Formatting data
  + Do all collection systems produce data in a format that is useful for detection?
+ Normalizing data
  + Is the data normalized to a common schema or data model?
  + Is the data normalized before or after it is written to persistent storage?
+ Decorating data
  + Does the system provide the ability to enrich data?
  + Does the system integrate with external tools or services used by the team?

### Data Analytics

Provides the ability to apply detection methods to, implement alerting strategies on, and visualize data.

Key considerations:

+ Detection methods
  + Which detection methods are supported?
  + Is the system able to support custom detection methods?
  + How are detection methods managed (e.g., in console, as code)?
+ Alerting strategies
  + Which alerting strategies are supported?
  + How does the team decide which alerting strategy to use?

### Monitoring & Metrics

Provides the ability to monitor the health of the detection platform.

## Detection Metrics

Metrics used to measure the effectiveness of a detection engineering program.

### Coverage

#### Detection Coverage

Detection coverage metrics provide insight into detections that are active and generating alerts or metadata. These metrics should map detections to business environments, critical assets, or threat models; detections can also be mapped to visibility domains, data sources, or threat frameworks, but these mappings do not indicate the worth of a detection.

Growth-phase detection engineering programs may measure coverage using a stoplight model (e.g., red, yellow, green) while mature programs should measure coverage using a count (in the case business environments or critical resources) or percentage (e.g., 80%; in the case of threat models) based on active detections. See the Data Coverage section for an example using a stoplight model.

#### Data Coverage

Data coverage metrics provide insight into data that is available for detection engineering. These metrics should map visibility domains and data sources to business environments.

Growth-phase detection engineering programs may measure coverage using a stoplight model (e.g., red, yellow, green) while mature programs should measure coverage using a percentage (e.g., 80%) based on observed data.

Below is an example using a stoplight model to measure corporate and production business environments:

| Business Environment | Visibility Domain | Data Source | Coverage |
| -------- | ------- | ------- | ------- |
| Corporate | Host | EDR | :green_apple: |
| Corporate | Network | N/A | :tomato: |
| Production | Cloud | CloudTrail | :lemon: |
| Production | Host | N/A | :tomato: |
| Production | Network | VPC Flow Logs | :green_apple: |
| Production | Network | Load Balancer Logs | :lemon: |

Since no single data source provides full visibility into a domain, it is usually necessary to layer multiple data sources to achieve full coverage in a single domain, and some tools may provide coverage across multiple domains.

### Reliability

#### Detection Reliability

Detection reliability metrics track the consistency of detections over time. These can be measured by purposefully triggering the detection logic or by observing the detection logic in production, and are best measured using a percentage (e.g., 80%) that can roll up to a multi-dimensional reliability metric (e.g., reliability across data source, visibility domain, business environment).

#### Data Reliability

System reliability metrics track the consistency of data delivered to a detection system over time. Similar to detection reliability metrics, these can be measured by inserting and monitoring labelled data that is put into the system, and are best measured using a percentage (e.g., 80%).

### Timeliness

#### Detection Timeliness

Detection timeliness metrics track latency of detections and the team responsible for implementing them, including:

+ Time to detect (the time between when an activity of interest occurs and when it is detected)
+ Time to implement (the time between when intelligence is available and when it is implemented in detection logic)
+ Time to fix (the time between when a detection is broken and when it is fixed)

These metrics are best measured using time (e.g., 30 seconds, 5 days).

#### Data Timeliness

System timeliness metrics track the latency of data delivered to a detection system. These can be measured by observing data in production (from the time it is put into the system to the time it is available for detection) or by measuring the time it takes to process labelled data inside of the system, and is best measured using time (e.g., 30 seconds).

## Relationship to Other Domains

### Threat Intelligence

Produces enriched information that is applied during detection engineering.

### Incident Response

Consumes enriched data (e.g, alerts) that is produced by detection engineering.

### Threat Hunting

Acts as a research method for detection engineering.
