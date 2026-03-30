# Datadog

**Monitoring:** Continually watch the performance of an entity by evaluating the metrics collected from it. For example - website, software, infrastructure, servers, cloud services etc.
**What to Monitor:** website, network latency, uptime, throughput, success rate, error rate, CPU usage, etc.

**Datadog:** It is an observability service for cloud-scale applications, providing monitoring of servers, databases, tools, and services, through a SaaS-based data analytics platform.

**It covers wide range of monitoring:-**
- Infrastructure monitoring
- Database monitoring
- Cloud monitoring
- Log monitoring
- Application Performance monitoring
- Real User monitoring
- Container monitoring
- Security monitoring
- Synthetic monitoring
**Most Integrations:-**
- OS -> Windows, Linux, Mac
- Cloud -> AWS, Azure, GCP
- Containers -> Docker, Helm, Container-d
- Messaging Services -> Kafka, Apache active MQ, hive MQ
- Security -> Alcide, Apptrail, Okta, Hashicorp vault.

-> Was founded in year 2010 by Olivier Pomel
-> Datadog's agent code is open-sourced on Github.

### Monitoring tool Requirements:-
- Data collection
- Data storage
- Querying & Analysis
- Visualization and Alerting
- Scalability and Performance
- Integration & Extensibility 
- Security and Access Control

**Alternative: Prometheus, InfluxDb, Nagios, Sensu, Dynatrace, Graphite, New relic**

## Basic Terminologies
1. **HOST:** it is an entity which datadog has to monitor. example. servers, VMs, containers, IOT devices, Desktops, etc.
2. **Metric:** it is a time bound information pertaining to a system captured at a certain point in time.
**TYPES:-**
	- WORK METRICS: Indicate the top-level health of your system by measuring its useful output.
		- Throughtput
		- Success rate
		- Error rate
		- Performance
	- Resource Metrics: Indicate timely information of physical resource components such as CPU, memory, disks.
		- Utilization
		- Saturation
		- Availability
		- Errors
3. **Events:** It happens at infrequent occurrences that usually provides the details of a change that happened in the system.
4. **Agent:** It is a service that runs alongside the application software system/host to collect various events and metrics from it and sends it to the datadog backend via internet.

### Architecture
![](./images/datadog/1_datadog_architecture.png)

Host the client side and the datadog backend side. Host is a datadog agent which is a lightweight software which runs on host. 
Datadog agent is the core of data monitoring solution as it is responsible for collecting the events, matrics and logs from the host and sending them to data backend to which users interact and based on the requirements the metrics can be filtered, grouped and converted to dashboards.
So basically we can say agent as middle layer between the host and the data lock software, which is hosted on cloud.
Datadog agent is comprised of 2 component the **collector** and **forwarder**. Collector is in charge of running checks and collection metrics from the hosts. It gathers all the standard metrics every 15secs and the forwarder takes the payloads from the collector and sends it to datadog over HTTPS this is via internet using port **443**. And also to optimize the communication there is a **buffer ** attached to the forwarder.
When a certain limit in size or number of outstanding send requests are reached in the buffer, they are released to datadog backend.
Datadog agent can be a **dogStatsD** the service as well as it is optional. **DogstatsD** an implementation of statsD protocol is a metrics aggregation service bundled with the datadog agent to send custom metrics from your application to datadog backend.
**HOW DogstatsD works:** If we have python application or java or any other instrumented application then dogstatsD accepts custom metrics, events and service checks over UDP periodically aggregates them and ultimately forwards them to datadog. Now since it uses UDP your application can send metrics to datastatsDX and resume its work without waiting for a response.
NOW there are 3 more optional processes that can be spawned by the agent if enabled in the configuration file. 1st is the **IPM agent**, which is a process to collect traces, and the 2nd is **Process Agent** which is a process to collect live process information by default it only collects available containers otherwise it is disabled. 3rd is **UI Agent** this is the UI side of datadog agent. To see the details of datadog agent in UI, then there is option of its UI component which runs directly on the host where the datadog agent is running.
TO view the datadog agent's UI you have to configure the port on which the GUI should run in the datadog yml file. For windows and Mac the UI is already enabled by default and it runs on PORT 5002.

**Summary**: At first we install a datadog agent it can be integration service or dogstatsD on the host system. After installation, the collector part of it starts collecting data that is the metrics, events, logs or whatever from the host. And the forwarder components shifts the collector data to the cloud via memory buffer through circular HTTPS connections. Once the data reached the datadog backend users can access the datadog website and perform aggregations on that data or filter them trigger alerts to the users or create dashboards and less other activities can be performed using that data to generate meaningful insights.


**HOW datadog agent works?**

The datadog agent is software that runs on your hosts. After installation it automatically starts to collects events and metrics from hosts and sends them to datadog, where you can search, filter, aggregate and alert on information. The datadog agent acts like a middle layer between you application and datadog website.


**THE main components are:-**

1. **Collector:** which collect data from your host on every 15 seconds

2. **Forwarder:** which sends data to datadog over https

Configuration files for integrations are in: `C\ProgramData\Datadog\conf.d`

The main configuration file is: `C\ProgramData\Datadog\datadog.yaml`


**MONITORING SERVICES:-**

For monitoring services, a good practice is to monitor the RED metrics (Rate, errors, and duration).

1. Rate: Monitor the number of requests your service receives.
2. Errors: Track how many of those requests fail.
3. Duration: Measure how long those requests take (latency).

**Here are examples of Datadog monitors types you can create to monitor your services:**

- **Metric**: Compare values of a metric with a user-defined threshold.
- **Logs**: Alert when a specified type of log exceeds a user-defined threshold over a given period of time.
- **Database Monitoring**: Monitor query execution and explain plan data gathered by Datadog.
- **Error Tracking:** Monitor issues in your applications gathered by Datadog
- **Real User Monitoring:** Observe user behavior and monitor frontend performance.
- **Synthetic Monitoring:** Simulate user actions to test API endpoints or website functionality.
- **Anomaly**: Detect anomalous behavior for a metric based on historical data.
-**Cloud Network Monitoring:** Monitor cloud-specific network configurations and traffic.



### TAGGING 
Tags are a way of adding dimensions to Datadog telemetries so they can be filtered, aggregated, and compared in datadog visualizations.
Datadog tagging binds metric, traces, and logs under one name thereby allowing for correlation and call to action between them. Defined as key-value pair.

**TAGS CAN BE CONFIGURED IN SEVERES WAYS:-**
- DatadogUI 
- datadog.yaml 
- integration configuration file(confs.d) 
- datadog API
- DogStatsD

### INFRASTRUCTURE
Datadog live processes gives real-time visibility into the processes running on your infrastructure. Datadog automatically collects and passes all of your processes across your on-prem hybrid or cloud native infrastructure in real-time.
`Infrastructure --> Processes:` Here we can view all of our running processes in one place. In this view it includes two graphs, time series and scatterplot graph.

`Infrastructure Monitoring- Container`: Container are lightweight packages of software that contain all of the necessary elements to run in any environment. It virtualize the operating system and runs anywhere from a private data center to the public cloud.

### METRICS
Information(the data numbers) pertaining to your system captured at a certain point in time. Metric is time-bound and its value will change.
Example: app.latency [3.34, 22:11:01] in 11 at night the latency is 3.34.

**Metric sources:-**

**1. The Datadog Agent**
- Agent-based integrations
- DogStatsD

**2. Datadog Integrations**
**3. Other areas of the Datadog platform**
- Real User Monitoring (RUM)
- Application Performance Monitoring (APM)
- Logs
- Processes
- Events

**4. The Datadog API**

**TYPES OF METRICS:-**
Affects how the metric values are displayed when queried, as well as the associated graphing possibilities. Metric's type determines how the values collected by the agent are aggregated for submission over a particular time interval.

1. **Count**: Count metrics measure the total number of events within a specific period. They are represented as integers.
Example: users.active_users [1,2,1,4,1,1,5,1] --> users.active_users [16]

2. **Rate**: Rate metrics measure the number of events occurring per second during a given time interval. They track the frequency of events over time, rather than their cumulative count. Rates are represented as integers.
Rate total count in the interval/length of the time interval
Example: users.active_users [1,2,1,4,1,1,5,1] --> users.active_users [1.6]

3. **Gauge**: Gauge metrics represent the last value received during the specific time period. Think of it as reading a speedometer in a vehicle, or your thermostat at home; it's an instantaneous value.
Example: system.temperature [71,71,71,71,71,71.5] --> system.temperature [71.5]

4. **Histogram**: Histogram metrics capture the statistical distribution of a set of values over a period of time. This depicts how frequently values fall into different ranges.


5. **Distribution**: It represents the global statistical distribution of a set of values calculated across entire distributed infrastructure/all hosts in one time interval. It sends all the raw data during a time interval to datadog.

SEEE LECTURE AND TAKE SS 8.2

The agent aggregates multiple data points for each unique metric into a single data point over a period of time called the flash interval, which for dogstatsD if of 10 seconds. The agent combines these values into a single representative metric value for that interval while assigning a single timestamp to it. And now this aggregated value with a single timestamp is sent to data servers for further aggregations.

**Metrics Summary:** It shows all the metrics reporting across your infrastructure under a specified time frame.
**Metrics Explorer:** It is a basic interface for examining your metrics in datadog. We can view the basic graph per metric here.

### CUSTOM METRICS - AGENT CHECK

IT is a metrics by default not present in our system. We first explicitly create a metric to solve any special use case which is then picked up by the datadog agent. Any metric sent using DogStatsD or via a custom agent check is considered as custom metric.

Useful in monitoring critical application KPIs like:-
- numbers of visitors on website
- average customer cart size
- Request latency
- Performance distribution

Custom metric can be sent to datadog using multiple Sybmission type:-
- Agent Check
- count
- Gauge
- Rate
- Histogram
- DogstatsD
- Powershe11
- API

### EVENTS 
It represent a notable change in the state of a monitored application or device.
For example:-
- Error or exception generated by the application.
- Performance threshold cross.
- Configuration changes in the environment.
- Operational changes in the application such as a JVM restart.

Events are generated from Datadog agent (automatic), 100+ supported integrations (Kubernetes, Docker, Jenkins, AWS ECS and Nagios) and custom events (Datadog API, Custom Agent Check, DataStatsD).

Can generate metrics from any event search query with 15-month retention.

### DATADOG INTEGRATIONS

**TYPES OF INTEFRATIONS:-**

**1. Agent-based Integrations:** Agent-based integrations are run with the Datadog Agent on your host or in containers, and use a Python class method called check to define the metrics to collect. Datadog's default Agent-based integrations provide the capacity to monitor the major components of an organization's infrastructure by collecting performance data for disk, CPU, memory, network throughput, and more.


**2. Authentication (Crawler-based) Integration:** are configured in Datadog and require you to provide credentials to obtain metrics and data through an API. These include popular integrations for Slack, AWS, Azure, and PagerDuty. These integrations are referred to as "crawler integrations" because they use the credentials you provide to crawl through your infrastructure and collect data.

**3. Library Integration:** often referred to as trace libraries, enable you to monitor applications based on the language they're written in, such as Node.js or Python. These libraries are installed in your application code and send data to the Datadog Agent. The Datadog Agent then sends the application metrics, traces, and logs to Datadog with related tags.



Application Performance Management(APM):- The translation of IT metrics into business meaning. A practive to monitor application insights, so we can improve performance, improve user experience, reduce issues and errors.
