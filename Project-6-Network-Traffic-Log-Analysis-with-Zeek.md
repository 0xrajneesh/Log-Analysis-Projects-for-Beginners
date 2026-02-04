# Project 6: Network Traffic Log Analysis Using Zeek and PCAP Files

## Introduction

In this project, students will learn how to analyze network traffic logs using Zeek (formerly Bro) and packet capture (PCAP) files. Network traffic analysis is a critical skill for Security Operations Center (SOC) analysts to detect suspicious activity such as port scanning, malware communication, lateral movement, and data exfiltration.

By the end of this project, you will be able to generate Zeek logs from PCAP files, interpret key log types, and identify potential security incidents.

---

## Pre-requisites

- Basic networking knowledge (TCP/IP, DNS, HTTP)
- Familiarity with Linux command line
- Ubuntu 22.04 or later (or any Linux distro)
- Wireshark installed (optional but helpful)
- Zeek installed

---

## Lab Setup and Tools

- Ubuntu Linux VM or physical machine
- Zeek Network Security Monitor
- Sample PCAP files (from malware-traffic-analysis.net or similar sources)
- Terminal access

---

## Exercise 1: Installing Zeek

### Steps:

1. Update system packages:
   ```bash
   sudo apt update && sudo apt upgrade -y
````

2. Install Zeek:

   ```bash
   sudo apt install zeek -y
   ```

3. Verify installation:

   ```bash
   zeek --version
   ```

---

## Exercise 2: Analyzing a PCAP File

### Steps:

1. Create a working directory:

   ```bash
   mkdir zeek-lab && cd zeek-lab
   ```

2. Copy your PCAP file into the folder.

3. Run Zeek against the PCAP:

   ```bash
   zeek -r sample.pcap
   ```

4. List generated logs:

   ```bash
   ls
   ```

---

## Exercise 3: Understanding Zeek Logs

### Common Log Files:

* `conn.log` – Network connections
* `dns.log` – DNS queries
* `http.log` – HTTP traffic
* `ssl.log` – TLS sessions
* `files.log` – Transferred files
* `notice.log` – Alerts and detections

### View logs:

```bash
less conn.log
less dns.log
less http.log
```

---

## Exercise 4: Detecting Suspicious Activity

### Tasks:

* Identify top source IPs:

  ```bash
  cat conn.log | zeek-cut id.orig_h | sort | uniq -c | sort -nr | head
  ```

* Look for port scanning:

  ```bash
  cat conn.log | zeek-cut id.resp_p service | sort | uniq -c | sort -nr
  ```

* Suspicious DNS queries:

  ```bash
  cat dns.log | zeek-cut query | sort | uniq -c | sort -nr | head
  ```

* Find downloaded executables:

  ```bash
  cat files.log | zeek-cut mime_type filename
  ```

---

## Exercise 5: Investigating Alerts

### Steps:

1. Open notice log:

   ```bash
   less notice.log
   ```

2. Identify:

   * Scans
   * Weird protocols
   * Suspicious domains
   * Malware indicators

---

## Expected Outcome

After completing this project, you should be able to:

* Run Zeek against PCAP files
* Understand major Zeek log types
* Detect abnormal network behavior
* Identify possible malware communication
* Perform initial SOC-style triage

---

## Bonus Challenge

* Import Zeek logs into ELK or Splunk
* Visualize top talkers
* Build detection queries
* Create a short incident report

---

## Real-World SOC Use Case

SOC analysts regularly use Zeek for:

* Threat hunting
* Network forensics
* Intrusion detection
* Traffic baselining
* Malware analysis

This project simulates a real SOC investigation workflow.

