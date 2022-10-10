# Detection Engineering Pocket Guide

## Table Of Contents

[Definitions](#definitions)

[Methodology](#methodology)

[Visibility](#visibility)

+ [Domain](#domain)
+ [Collection](#collection)
+ [Permanence](#permanence)

[Implementations](#implementations)

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

## Implementations

Methods used to implement detection logic. These methods can be combined to create high complexity logic.

### Match

Triggers detection by alerting on a series of string or regular expression matches.<br>
<br>
Example: fieldX == "foo" and fieldY == /bar$/

### Aggregate

Triggers detection by alerting when a variable breaches a threshold according to an aggregation function. The most common aggregation is a count that exceeds a static threshold, but more complex aggregations may use statistical functions such as min, max, and standard deviation.<br>
<br>
Example: "foo" appeared more than 10 times over a period of 30 seconds

### Join

Triggers detection by alerting when activities of interest coalesce on a variable across multiple events.

Example: fieldX == "foo" in eventA AND fieldX == "bar" in eventB ON fieldY over a period of 1 minute

## Relationship to Other Domains

### Threat Intelligence

Produces enriched information that is consumed during detection engineering.

### Incident Response

Consumes enriched data that is produced by detection engineering.

### Threat Hunting

Acts as a research method for detection engineering.
