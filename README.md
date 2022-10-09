# Detection Engineering Pocket Guide

## Relationship to Other Domains
### Threat Intelligence
Produces enriched information that is consumed during detection engineering.

### Incident Response
Consumes enriched data that is produced by detection engineering.

### Threat Hunting
Acts as a research method for detection engineering.

## Visibility
Visibility describes the availability and applicability of data used in detection engineering and security operations. There is no detection engineering without sufficient visibility.

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
Contains data that describes traits of and actions taken in a cloud service provider.<br>
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
This is rarely useful for proactive threat detection and is better used for reactive threat assessments.

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
