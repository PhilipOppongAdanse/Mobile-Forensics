# Android Device Analysis Using Android Debug Bridge (ADB)

## Overview

In this project, I performed a forensic examination of an Android device using Android Debug Bridge (ADB) from a Kali Linux virtual machine. The objective was to collect and analyze device information, enumerate installed applications, extract system logs, review device usage statistics, and document artifacts that could support a digital forensic investigation.

ADB provides investigators with a command-line interface to communicate directly with Android devices. When USB Debugging is enabled, it becomes possible to gather a wide range of system information without requiring third-party forensic tools.

---

## Investigation Objectives

The primary objectives of this examination were to:

- Establish communication between the Android device and forensic workstation.
- Identify device specifications and operating system details.
- Enumerate installed applications and package locations.
- Extract system logs for forensic review.
- Collect battery and power-related artifacts.
- Examine device usage statistics.
- Review application execution history.
- Identify boot-related information.
- Generate comprehensive system reports.
- Document the forensic acquisition process.

---

# Laboratory Setup

## Forensic Workstation

| Item | Description |
|--------|-------------|
| Operating System | Kali Linux |
| Environment | VMware Workstation |
| Acquisition Method | Android Debug Bridge (ADB) |
| Investigation Type | Android Device Examination |

---

## Evidence Device

| Attribute | Value |
|------------|---------|
| Device Name | itel P55 |
| Model | itel A666L |
| Android Version | Android 13 |
| CPU | Unisoc T606 (UMS9230) |
| RAM | 8 GB |
| Internal Storage | 128 GB |
| Battery Capacity | 5000mAh |

---

# Evidence Documentation

## Examination Environment

The Android device was connected to a forensic workstation running Kali Linux through VMware Workstation. Communication was established through Android Debug Bridge (ADB) after enabling USB Debugging on the device.

### Examination Setup

![Forensic Setup](images/16-device-front-image.jpg)

The image above shows the Android device connected to the forensic workstation during acquisition.

---

## Device Rear View

![Device Rear View](images/17-device-back-image.jpg)

The rear view of the evidence device was documented to preserve its physical condition and identifying characteristics before analysis.

---

## Device Specifications

![Device Specifications](images/18-device-specification.jpg)

The device specification page was captured to verify hardware and operating system information directly from the device.

---

# Methodology

The examination followed a structured workflow:

1. Verify ADB connectivity.
2. Identify device properties.
3. Enumerate installed applications.
4. Extract system logs.
5. Review battery information.
6. Analyze device usage statistics.
7. Review application activity history.
8. Examine power management artifacts.
9. Identify boot-related information.
10. Generate system diagnostic reports.

---

# Step 1: ADB Connectivity Verification

Before any acquisition could occur, communication between the forensic workstation and the Android device was verified.

### Command

```bash
adb devices
```

### Screenshot

![ADB Verification](images/01-adb-connection-verification.png)

### Analysis

The device successfully appeared within the ADB device list.

This confirmed:

- USB Debugging was enabled.
- The workstation could communicate with the device.
- The device was ready for forensic examination.

---

# Step 2: Device Identification

Basic system information was collected to identify the device under examination.

### Commands

```bash
adb shell getprop ro.product.model

adb shell getprop ro.build.version.release

adb shell getprop ro.serialno
```

### Screenshot

![System Information](images/02-basic-system-info.png)

### Analysis

The commands returned information including:

- Device Model
- Android Version
- Serial Number
- Build Information

These artifacts are useful for evidence identification and chain-of-custody documentation.

---

# Step 3: Installed Application Enumeration

Installed applications were identified to determine software present on the device.

### Command

```bash
adb shell pm list packages -f
```

### Screenshots

![Installed Apps](images/03-installed-apps-and-path-01.png)

![Installed Apps](images/04-installed-apps-and-path-02.png)

![Installed Apps](images/05-installed-apps-and-path-03.png)

### Analysis

The output revealed:

- System applications
- Vendor-installed applications
- User-installed applications
- APK installation paths

Installed application enumeration is important because it helps identify:

- Potential communication platforms
- Social media applications
- Financial applications
- Suspicious software
- Malware indicators

---

# Step 4: System Log Acquisition

System logs were extracted to identify historical system activity.

### Command

```bash
adb logcat -d > system_logs.txt
```

### Screenshot

![System Logs](images/06-system-log-extraction.png)

### Analysis

System logs may contain:

- Application execution events
- System warnings
- Error messages
- Network activity
- Device events

Log files often assist investigators when reconstructing timelines.

---

# Step 5: Battery and Power Metrics

Battery information was collected using Android's built-in diagnostic framework.

### Command

```bash
adb shell dumpsys battery
```

### Screenshot

![Battery Information](images/07-battery-power-metrics.png)

### Analysis

Battery artifacts included:

- Battery level
- Charging status
- Battery health
- Voltage values
- Temperature readings

These artifacts may provide insight into device state during acquisition.

---

# Step 6: Device Usage Statistics

Android usage statistics were examined to identify user interaction patterns.

### Command

```bash
adb shell dumpsys usagestats
```

### Screenshot

![Usage Statistics](images/08-device-usage-stats.png)

### Analysis

Usage statistics may reveal:

- Frequently used applications
- Recent application activity
- Foreground application usage
- Device interaction patterns

These records can support user activity reconstruction.

---

# Step 7: Application Activity Timeline

Application execution information was reviewed to identify application usage history.

### Screenshot

![Application Timeline](images/09-device-application-timeline.png)

### Analysis

The extracted information may contain:

- Application launch timestamps
- Background execution events
- Session activity
- User interaction records

This information is valuable during timeline analysis.

---

# Step 8: Power Management Analysis

Power management exemptions were examined.

### Command

```bash
adb shell dumpsys deviceidle whitelist
```

### Screenshot

![Whitelist Analysis](images/10-power-white-listed-apps.png)

### Analysis

Applications found within the whitelist may:

- Operate continuously
- Ignore battery optimization
- Maintain persistent network access

These applications may warrant additional review during investigations.

---

# Step 9: Boot Count Analysis

Boot-related artifacts were collected to determine device restart history.

### Command

```bash
adb shell settings list global | grep boot_count
```

### Screenshot

![Boot Count](images/11-device-global-boot-time.png)

### Analysis

Boot count artifacts may indicate:

- Device restart frequency
- Operational history
- Potential anti-forensic activity
- Device maintenance events

---

# Step 10: System Diagnostic Collection

A comprehensive system report was generated.

### Command

```bash
adb shell dumpsys
```

### Screenshots

![System Report](images/12-dump-sys-report.png)

![System Report](images/13-system-report-01.png)

![System Report](images/14-system-report-02.png)

![System Report](images/15-system-report-03.png)

### Analysis

The `dumpsys` report contains extensive forensic information including:

- Running services
- Active processes
- Hardware configuration
- Device settings
- Memory usage
- Power statistics
- Network information
- System status

This dataset represents one of the richest sources of Android forensic artifacts accessible through ADB.

---

# Key Findings

During this examination I successfully obtained:

- Device identification information.
- Android operating system details.
- Installed application inventory.
- Application installation paths.
- System logs.
- Battery statistics.
- Device usage records.
- Application activity artifacts.
- Power management information.
- Boot history artifacts.
- Comprehensive system diagnostic reports.

---

# Forensic Value of ADB

Android Debug Bridge provides investigators with a powerful method of collecting information from Android devices when USB Debugging is available.

The tool enables:

- Rapid triage of Android devices.
- Device profiling.
- System artifact collection.
- Application enumeration.
- Timeline development.
- Operational analysis.

Although ADB does not replace full physical or file system acquisition tools such as Cellebrite, Magnet AXIOM, or Oxygen Forensics, it remains a valuable technique for preliminary examinations and laboratory exercises.

---

# Conclusion

This project demonstrated how Android Debug Bridge can be used to acquire and analyze forensic artifacts from an Android device running Android 13.

Using a structured forensic methodology, I established communication with the device, identified system properties, enumerated installed applications, collected logs, reviewed battery and usage statistics, examined power management artifacts, and generated comprehensive system reports.

The examination produced multiple categories of evidence that could support forensic investigations, incident response activities, and digital evidence analysis.

---

## Tools Used

- Kali Linux
- VMware Workstation
- Android Debug Bridge (ADB)
- Android 13 Device
- Linux Terminal

---

## Skills Demonstrated

- Android Forensics
- Mobile Device Examination
- Digital Evidence Collection
- Application Enumeration
- System Artifact Analysis
- Timeline Reconstruction
- Evidence Documentation
- Log Analysis
- Device Profiling
- DFIR Methodology

---

### Author

**Phil Oppong**  
Digital Forensics & Incident Response (DFIR) Practitioner

