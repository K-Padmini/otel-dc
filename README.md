# ODCD (OpenTelemetry based Data Collector for Telemetry Data)

**[Semantic Convention](docs/semconv)** |
**[Support](docs/support/README.md)** |
**[Changelog](CHANGELOG.md)** |
**[Contributing](CONTRIBUTING.md)** |
**[License](LICENSE)**

---
ODCD (OpenTelemetry based Data Collector for Telemetry Data) is a collection of stanalone OpenTelemetry receivers for databases, systems, and apps. All implementations are based on predefined OpenTelemetry Semantic Conventions. A standard OTLP exporter is provided to forward the data from this "Data Collector" to a Telemetry backend or an OpenTelemetry Collector.

<br><br>

# Data Collector for Databases


## Requirements

- Java 8+

## Build & Installation

1) Make sure Java SDK 8+ is installed.
```bash
java -version
```

2) Get the source code from `github.com`.
```bash
git clone https://github.com/instana/otel-dc.git
cd otel-dc/rdb
```

3) Build with Gradle
```bash
./gradlew clean build
```
*Note: gradle 7.4 will be installed if you do not have it.*

## Run

1) Make sure code is built with Java SDK 8+.

2) Refine configuration file (config/config.yaml) according to your own database. Right now we provide Data Collector for following databases:
  - DaMeng database
  
  >*Note: We respect the OTel community conventions and consider more about popular database engines for conventionss. While we may create 
  > implementations from those databases without OTel support based on user requirements or developer contributions. *

3) Start up your OTLP backend which accept OTLP connections. Right now we support following protocols:
- otlp/grpc

4) Option-1: Run the Data Collector with gradle
```bash
./gradlew run
```
5) Option-2: Find the deployment package (otel-dc-rdb-*.tar) generated by gradle in the "build/distributions/" directory, extract deployment files:
```bash
cd build/distributions/
tar vxf otel-dc-rdb-*.tar
rm -f *.tar *.zip
cd otel-dc-rdb-*
```

Then, make sure following configuration files are correct for your environment.:
  - config/config.yaml
  - config/logging.properties

Run the Data Collector with following command according to your current OS:
```bash
bin/otel-dc-rdb
```

*Note:* The default configuration file is config/config.yaml, you can also use environment variable "DC_CONFIG" to speficy the configuration file, for example:
```bash
export DC_CONFIG=config/config-oceanbase.yaml
bin/otel-dc-rdb
```


## Create Data Collector implementation for a new database

Please refer to "[How to create data collector implementation for a new database](docs/developer/new-db.md)".