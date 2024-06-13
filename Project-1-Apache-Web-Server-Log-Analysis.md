# Project 1: Basic Apache Web Server Log Analysis

## Introduction
In this project, students will learn the fundamentals of log analysis by working with Apache web server logs. Apache logs are a rich source of information about web traffic and can help identify potential security incidents, usage patterns, and performance issues. By the end of this project, students will be able to extract and interpret valuable information from Apache access and error logs.

## Pre-requisites
- Basic understanding of web servers and HTTP protocols
- Familiarity with Linux command line
- Apache web server installed (can be on a local machine or a VM)

## Lab Set-up and Tools
- Ubuntu 22.04 or later (or any Linux distribution with Apache installed)
- Apache web server installed and running
- Access to Apache log files (typically located in `/var/log/apache2/`)

## Exercises

### Exercise 1: Accessing Apache Log Files

**Steps:**

1. Open a terminal on your Linux machine.
2. Navigate to the Apache log directory:
    ```bash
    cd /var/log/apache2/
    ```
3. List the log files to understand the available logs:
    ```bash
    ls -l
    ```

**Expected Output:**
- A list of Apache log files such as `access.log` and `error.log`.

### Exercise 2: Understanding Access Logs

**Steps:**

1. Open the access log file using `less` or `cat`:
    ```bash
    less access.log
    ```
2. Observe the format of the log entries, which typically include information such as IP address, request timestamp, request method, URL, HTTP status code, and user agent.
3. Identify a few entries and break down their components.

**Expected Output:**
- Understanding of the structure of access log entries, including IP addresses, timestamps, request methods, URLs, status codes, and user agents.

### Exercise 3: Filtering Log Entries

**Steps:**

1. Use the `grep` command to filter log entries based on specific criteria, such as a particular IP address:
    ```bash
    grep '192.168.1.100' access.log
    ```
2. Filter log entries by HTTP status code (e.g., 404 errors):
    ```bash
    grep ' 404 ' access.log
    ```
3. Combine filters to extract more specific information, such as 404 errors from a specific IP address:
    ```bash
    grep '192.168.1.100' access.log | grep ' 404 '
    ```

**Expected Output:**
- A filtered list of log entries matching the specified criteria, demonstrating how to extract specific information from log files.

### Exercise 4: Analyzing Error Logs

**Steps:**

1. Open the error log file using `less` or `cat`:
    ```bash
    less error.log
    ```
2. Identify different types of errors, such as file not found errors, script errors, or permission issues.
3. Note the timestamps and frequency of errors to understand patterns or recurring issues.

**Expected Output:**
- Insight into the types of errors logged in the error log, including their causes and frequency.

### Exercise 5: Summarizing Log Data

**Steps:**

1. Use the `awk` command to summarize log data, such as counting the number of requests from each IP address:
    ```bash
    awk '{print $1}' access.log | sort | uniq -c | sort -nr
    ```
2. Summarize the number of requests per day:
    ```bash
    awk '{print $4}' access.log | cut -d: -f1 | sort | uniq -c
    ```
3. Identify the most requested URLs:
    ```bash
    awk '{print $7}' access.log | sort | uniq -c | sort -nr
    ```

**Expected Output:**
- Summarized log data showing the number of requests per IP address, the number of requests per day, and the most requested URLs.

By completing these exercises, students will gain hands-on experience in accessing, filtering, and analyzing Apache web server logs, which are essential skills for identifying security incidents, understanding web traffic patterns, and troubleshooting issues.
