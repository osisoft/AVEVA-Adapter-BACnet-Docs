---
uid: ReleaseNotes
---
# Release notes

[!include[product-name](../main/shared-content/_includes/inline/product-name.md)] [!include[product-version](../main/shared-content/_includes/inline/product-version.md)]<br/>
Adapter Framework [!include[framework-version](../main/shared-content/_includes/inline/framework-version.md)]

## Overview

PI Adapter for BACnet collects time-series data from source devices to OMF endpoints in OSIsoft Cloud Services or PI Servers. PI Adapter for BACnet can also collect health and diagnostics information. It supports buffering, polled and unsolicited data collection, automatic discovery of available data items on a data source, and various Windows and Linux-based operating systems as well as containerization.

For more information, see [PI Adapter for BACnet overview](xref:PIAdapterforBACnetOverview).

## New features

| Feature | Description |
|--|--|
| Discovery | PI Adapter for BACnet now includes _discovery_, which allows you to query for devices on your network and automatically create a data selection configuration. For more information, see <xref:DiscoveryConfiguration>. |
| Productized data property types and handling | PI Adapter for BACnet can now send units of measure for simple types when you configure them for a stream at source. You can configure container-level overrides by setting the `IncludeProperties` parameter within your data source configuration to `true`. For more information, see [Data source parameters](xref:PIAdapterforBACnetDataSourceConfiguration#data-source-parameters). |

## Resolved issues

This release includes various resolved issues and security improvements.

## Known issues

There are no known issues at this time.

## System requirements

Refer to <xref:SystemRequirements>.

## Installation and upgrade

Refer to <xref:InstallTheAdapter> or <xref:UpgradeTheAdapter>.

### Linux installation note

BACnet protocol uses UDP/IP socket communication. Linux places restrictive limits (212992 bytes) on the size of receive buffers of sockets, and this restriction limits the performance of the PI Adapter for BACnet on Linux.

Enter the following commands to check the current UDP/IP receive buffer settings:

```bash
$ sysctl net.core.rmem_max
net.core.rmem_max = 212992
$ sysctl net.core.rmem_default
net.core.rmem_default = 212992
```

If the values are less than 26214400 bytes (25MB), add the following two lines to the `/etc/sysctl.conf` file:

```text
net.core.rmem_max=26214400
net.core.rmem_default=26214400
```

Save the file and reboot the machine, then proceed with [installation](xref:InstallTheAdapter#linux).

## Uninstallation

Refer to the [Uninstall the adapter](xref:UninstallTheAdapter).

## Security information and guidance

### OSIsoft's commitment

Because the PI System often serves as a barrier protecting control system networks and mission-critical infrastructure assets, OSIsoft is committed to (1) delivering a high-quality product and (2) communicating clearly what security issues have been addressed. This release of PI Adapter for BACnet is the highest quality and most secure version of the PI Adapter for BACnet released to date. OSIsoft's commitment to improving the PI System is ongoing, and each future version should raise the quality and security bar even further.

### Vulnerability communication

The practice of publicly disclosing internally discovered vulnerabilities is consistent with the Common Industrial Control System Vulnerability Disclosure Framework developed by the Industrial Control Systems Joint Working Group (ICSJWG). Despite the increased risk posed by greater transparency, OSIsoft is sharing this information to help you make an informed decision about when to upgrade to ensure your PI System has the best available protection.

For more information, refer to [OSIsoft's Ethical Disclosure Policy](https://www.osisoft.com/ethical-disclosure-policy).

To report a security vulnerability, refer to [OSIsoft's Report a Security Vulnerability](https://www.osisoft.com/report-a-security-vulnerability).

### Vulnerability scoring

OSIsoft has selected the Common Vulnerability Scoring System (CVSS) to quantify the severity of security vulnerabilities for disclosure. To calculate the CVSS scores, OSIsoft uses the National Vulnerability Database (NVD) calculator maintained by the National Institute of Standards and Technology (NIST).  OSIsoft uses Critical, High, Medium, and Low categories to aggregate the CVSS Base scores. This removes some of the opinion related errors of CVSS scoring.  As noted in the CVSS specification, Base score range from 0 for the lowest severity to 10 for the highest severity.

### Overview of new vulnerabilities found or fixed

This section is intended to provide relevant security-related information to guide your installation or upgrade decision. OSIsoft is proactively disclosing aggregate information about the number and severity of PI Adapter for BACnet security vulnerabilities that are fixed in this release.

No security-related information is applicable to this release.

## Technical support and resources

Refer to [Technical support and feedback](xref:TechnicalSupportAndFeedback).
