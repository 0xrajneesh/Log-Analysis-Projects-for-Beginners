# Lab: Analyzing Windows Sysmon Events for Security Incidents

## Introduction

In this lab, you will learn how to analyze Windows Sysmon (System Monitor) events for security incidents. Sysmon is a powerful Windows system service and device driver that logs system activity to the Windows Event Log, providing detailed information on process creations, network connections, file changes, and more. By examining these logs, you can identify suspicious activities and potential security incidents.

## Pre-requisites

- Basic understanding of Windows operating system and its components.
- Familiarity with basic cybersecurity concepts.
- A computer running Windows 10 or later (virtual machine recommended for safety).
- Internet connection to download necessary tools.

## Lab Set-up and Tools

1. **Install Sysmon**:
   - Download Sysmon from the [Sysinternals website](https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon).
   - Extract the downloaded file.

2. **Configure Sysmon**:
   - Download a Sysmon configuration file. You can use the official SwiftOnSecurity configuration file from [GitHub](https://github.com/SwiftOnSecurity/sysmon-config).
   - Open Command Prompt with administrative privileges and navigate to the directory where Sysmon was extracted.
   - Install Sysmon with the configuration file:
     ```bash
     sysmon -accepteula -i sysmonconfig-export.xml
     ```

3. **Tools**:
   - Sysmon (System Monitor)
   - Event Viewer (built-in Windows tool)
   - PowerShell (built-in Windows tool)

## Exercises

### Exercise 1: Verify Sysmon Installation and Configuration

1. **Objective**: Ensure that Sysmon is installed and configured correctly.

2. **Steps**:
   - Open Event Viewer by searching for it in the Start menu.
   - Navigate to `Applications and Services Logs -> Microsoft -> Windows -> Sysmon`.
   - Check for recent events to confirm that Sysmon is logging events.

3. **Expected Output**:
   - You should see a series of Sysmon events in the Event Viewer, indicating that Sysmon is actively monitoring the system.

### Exercise 2: Analyze Process Creation Events

1. **Objective**: Identify suspicious process creation events.

2. **Steps**:
   - Open Event Viewer and navigate to `Applications and Services Logs -> Microsoft -> Windows -> Sysmon -> Operational`.
   - Look for events with `Event ID 1` which indicate process creation.
   - Examine the details of the events, paying close attention to:
     - Parent process name
     - Process name
     - Command line arguments

3. **Expected Output**:
   - Identify any unusual or unexpected processes, such as unknown executables or processes started with suspicious command line arguments.

### Exercise 3: Monitor Network Connections

1. **Objective**: Detect suspicious network connections.

2. **Steps**:
   - In Event Viewer, navigate to `Applications and Services Logs -> Microsoft -> Windows -> Sysmon -> Operational`.
   - Look for events with `Event ID 3` which indicate network connections.
   - Review the details of the events, focusing on:
     - Source IP and port
     - Destination IP and port
     - Process responsible for the connection

3. **Expected Output**:
   - Identify any connections to known malicious IP addresses or unexpected external connections.

### Exercise 4: Investigate File Creation Events

1. **Objective**: Track down suspicious file creation activities.

2. **Steps**:
   - In Event Viewer, navigate to `Applications and Services Logs -> Microsoft -> Windows -> Sysmon -> Operational`.
   - Look for events with `Event ID 11` which indicate file creation.
   - Check the details of the events, including:
     - File path
     - File name
     - Process that created the file

3. **Expected Output**:
   - Detect any unusual file creation events, especially in sensitive directories or by untrusted processes.

### Exercise 5: Detecting Image Load Events

1. **Objective**: Identify suspicious DLL or EXE image load activities.

2. **Steps**:
   - In Event Viewer, navigate to `Applications and Services Logs -> Microsoft -> Windows -> Sysmon -> Operational`.
   - Look for events with `Event ID 7` which indicate image load.
   - Analyze the details of the events, including:
     - Image path
     - Process that loaded the image

3. **Expected Output**:
   - Uncover any unexpected or unauthorized image loads that could indicate malicious activity, such as DLL injection.

## Conclusion

By completing these exercises, you should now have a basic understanding of how to use Sysmon and Event Viewer to monitor and analyze Windows events for potential security incidents. Regular monitoring and analysis of Sysmon logs can significantly enhance your ability to detect and respond to suspicious activities on Windows systems.
