# Project 4: Simple Log Analysis with ELK Stack (Elasticsearch, Logstash, Kibana)

## Introduction
In this project, students will learn the basics of log analysis using the ELK Stack, a popular open-source suite for managing and analyzing log data. The ELK Stack consists of Elasticsearch (for storing and searching data), Logstash (for processing and ingesting data), and Kibana (for visualizing data). By the end of this project, students will be able to set up the ELK Stack, ingest log data, and create visualizations to analyze the data.

## Pre-requisites
- Basic understanding of log files and log management
- Familiarity with Linux command line
- A Linux machine (preferably Ubuntu 20.04 or later)
- Java installed on the machine

## Lab Set-up and Tools
- Ubuntu 20.04 or later
- [Elasticsearch](https://www.elastic.co/downloads/elasticsearch) installed
- [Logstash](https://www.elastic.co/downloads/logstash) installed
- [Kibana](https://www.elastic.co/downloads/kibana) installed
- Sample log files for analysis

## Exercises

### Exercise 1: Installing Elasticsearch

**Steps:**

1. Download and install Elasticsearch:
    ```bash
    wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.12.1-amd64.deb
    sudo dpkg -i elasticsearch-7.12.1-amd64.deb
    ```
2. Start the Elasticsearch service:
    ```bash
    sudo systemctl start elasticsearch
    sudo systemctl enable elasticsearch
    ```
3. Verify that Elasticsearch is running by accessing `http://localhost:9200` in a web browser.

**Expected Output:**
- Elasticsearch is installed and running, accessible at `http://localhost:9200`.

### Exercise 2: Installing Logstash

**Steps:**

1. Download and install Logstash:
    ```bash
    wget https://artifacts.elastic.co/downloads/logstash/logstash-7.12.1.deb
    sudo dpkg -i logstash-7.12.1.deb
    ```
2. Configure Logstash by creating a configuration file (`logstash-simple.conf`):
    ```bash
    sudo nano /etc/logstash/conf.d/logstash-simple.conf
    ```
    Add the following content to the configuration file:
    ```plaintext
    input {
      file {
        path => "/path/to/your/logfile.log"
        start_position => "beginning"
      }
    }
    output {
      elasticsearch {
        hosts => ["localhost:9200"]
      }
      stdout { codec => rubydebug }
    }
    ```
3. Start the Logstash service:
    ```bash
    sudo systemctl start logstash
    sudo systemctl enable logstash
    ```

**Expected Output:**
- Logstash is installed and configured to ingest log data and send it to Elasticsearch.

### Exercise 3: Installing Kibana

**Steps:**

1. Download and install Kibana:
    ```bash
    wget https://artifacts.elastic.co/downloads/kibana/kibana-7.12.1-amd64.deb
    sudo dpkg -i kibana-7.12.1-amd64.deb
    ```
2. Start the Kibana service:
    ```bash
    sudo systemctl start kibana
    sudo systemctl enable kibana
    ```
3. Verify that Kibana is running by accessing `http://localhost:5601` in a web browser.

**Expected Output:**
- Kibana is installed and running, accessible at `http://localhost:5601`.

### Exercise 4: Ingesting Log Data with Logstash

**Steps:**

1. Ensure that the log file specified in `logstash-simple.conf` exists and contains sample log data.
2. Check the Logstash logs to verify that log data is being ingested:
    ```bash
    sudo tail -f /var/log/logstash/logstash-plain.log
    ```
3. Confirm that data is being indexed in Elasticsearch by accessing the Elasticsearch API:
    ```bash
    curl -X GET "localhost:9200/_cat/indices?v"
    ```

**Expected Output:**
- Log data is ingested by Logstash and indexed in Elasticsearch, confirmed by checking the indices in Elasticsearch.

### Exercise 5: Creating Visualizations in Kibana

**Steps:**

1. Open Kibana in a web browser (`http://localhost:5601`).
2. Configure an index pattern to match the log data indexed by Logstash:
    - Navigate to "Management" > "Kibana" > "Index Patterns".
    - Create a new index pattern matching the Logstash index (e.g., `logstash-*`).
3. Explore the log data in the "Discover" tab to understand the available fields and data.
4. Create visualizations based on the log data:
    - Navigate to "Visualize" > "Create new visualization".
    - Choose a visualization type (e.g., bar chart, line graph) and configure it using the log data fields.
5. Save the visualizations and add them to a new dashboard in Kibana.

**Expected Output:**
- Visualizations created in Kibana, providing insights into the log data, with a dashboard displaying various visualizations.

By completing these exercises, students will gain hands-on experience in setting up and using the ELK Stack for log analysis, including installing and configuring Elasticsearch, Logstash, and Kibana, ingesting log data, and creating visualizations to analyze the data.
