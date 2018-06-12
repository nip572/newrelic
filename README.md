# newrelic# JMX Monitor for New Relic Infrastructure

## Summary

The JMX monitor connects remotely to configured JMX servers to fetch metrics.

The monitor connects to each remote JMX server specified in the plugin.json.


## Monitor requirements

1. Java Runtime version 1.7 or later


## Installation

Unzip the nr-jmx-monitor.tar.gz file into the monitor home folder.

```
cd {nr-jmx-monitor}
tar xvf  nr-jmx-monitor.tar.gz
```

The control script - run.sh and nr-jmx-service scripts - are used for starting, stopping and getting status.
Update start.sh as follows

* Edit the APP_HOME variable in the start.sh script.


### Setup the monitor to run as service

Setting up the application to run as a Java Service is dependent on the platform. Please contact your platform administrator for help setting this up.


## Configuration

### plugin.json

Rename the plugin.template.json to plugin.json. Edit all parameters to your environment. 

The "global" object can contain the overall plugin properties:

* "account_id" - your new relic account id. You can find it in the URL that you use to access newrelic. For example: https://rpm.newrelic.com/accounts/{accountID}/applications
* "insights_mode" - If this monitor is started in Insights mode, then the insights_insert_key here will be used to post metric events.
* "infra_mode" - If this monitor is started in Infra (or RPC) mode, then this section contains the RPC service listen port. The infra agent plugin can then connect this to port to query metrics.
* "proxy" - Enter the proxy setting in this section if a proxy is required. See more detail later on in this document.


The "agents" object contains an array of “agent” objects. Each “agent” object has the following properties.

* "name" – any descriptive name for the server
* "host" – hostname or IP for the remote JMX server
* "port" – port number that the JMX server is listening on
* "login" - true if JMX security is turned on
* "username" - username used to connection (optional if not needed)
* "password" – password used to connection (optional if not needed)

### jmx-config

The jmx-config-sample folder contains sample jmx configuration. Copy one or more configuration files as need to the jmx-config folder to activate them.

## Proxy settings

```
	"proxy": {
			"proxy_host": "enter_proxy_host",
			"proxy_port": 443,
			"proxy_username": "enter_proxy_username",
			"proxy_password": "enter_proxy_password"
	}
```


## Logging

The logging configuration can be controlled using the logback configuration file- ./config/logback.xml

Edit the following block of XML at the end of the logback.xml to change the log level (possible values are INFO, DEBUG, ERROR) and the log ouput(possible values are STDOUT, FILE)
```
    <logger name="com.newrelic" level="DEBUG" additivity="false">
        <appender-ref ref="STDOUT" />
    </logger>
```

## Metrics and Dashboarding
All metrics collected by this plugin are reported Insights. 







