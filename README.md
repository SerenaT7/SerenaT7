### Building a Secure SOC + Honeynet in Azure (Live Traffic)

#### Cloud Honeynet / SOC

![Intro](https://i.imgur.com/oGdBeu9.png)

#### Introduction

In this project, I've implemented a mini honeynet in Azure and integrated log sources into a Log Analytics workspace. Microsoft Sentinel is utilized to build attack maps, trigger alerts, and create incidents. The project involves measuring security metrics in an insecure environment for 24 hours, applying security controls, measuring metrics for another 24 hours, and presenting the results.

#### Architecture Before Hardening / Security Controls

##### Architecture Diagram

![ArchBefore](https://i.imgur.com/hcXZtQT.png)

#### Architecture After Hardening / Security Controls

##### Architecture Diagram

![ArchAfter](https://i.imgur.com/HxWLNTZ.png)

The architecture includes:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 Windows, 1 Linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were initially deployed and exposed to the internet. After applying security controls, Network Security Groups were hardened, and resources were protected by built-in firewalls and Private Endpoints.

##### Attack Maps Before Hardening / Security Controls

- NSG Allowed Inbound Malicious Flows
- Linux Syslog Auth Failures
- Windows RDP/SMB Auth Failures

#### Metrics Before Hardening / Security Controls

| Metric                      | Count  |
|-----------------------------|--------|
| SecurityEvent               | 32458  |
| Syslog                      | 4515   |
| SecurityAlert               | 4      |
| SecurityIncident            | 109    |
| AzureNetworkAnalytics_CL    | 2375   |

#### Attack Maps Before Hardening / Security Controls

All map queries returned no results due to no instances of malicious activity for the 24-hour period after hardening.

![NSGBefore](https://i.imgur.com/EnPjan6.png)

![Syslog](https://i.imgur.com/Q8mpmt6.png)

![RDP](https://i.imgur.com/SnYo5Hp.png)



#### Metrics After Hardening / Security Controls

| Metric                      | Count  |
|-----------------------------|--------|
| SecurityEvent               | 10198  |
| Syslog                      | 11     |
| SecurityAlert               | 0      |
| SecurityIncident            | 0      |
| AzureNetworkAnalytics_CL    | 10     |

#### GeoIP Information for Attacks

##### GeoIP for NSG Allowed Inbound Malicious Flows

![GeoIPNSG](https://imgur.com/XiMzRLy.png)

##### GeoIP for Linux Syslog Auth Failures

![GeoIPSyslog](https://imgur.com/MxG050m.png)

##### GeoIP for Windows RDP/SMB Auth Failures

![GeoIPRDP/SMB](https://imgur.com/MUSKMe0.png)

#### Conclusion

In this project, a mini honeynet was built in Microsoft Azure, log sources were integrated into a Log Analytics workspace, and Microsoft Sentinel was employed for alerting and incident response. The implementation of security controls led to a significant reduction in security events and incidents, showcasing the effectiveness of the measures.

It's important to note that if the resources were heavily utilized by regular users, more security events and alerts might have been generated within the 24-hour period following the implementation of security controls.

### Results

**Change after securing environment:**

| Metric                              | Change               |
|-------------------------------------|----------------------|
| Security Events (Windows VMs)       | -68.58%              |
| Syslog (Linux VMs)                  | -99.76%              |
| SecurityAlert (Defender for Cloud)   | -100.00%             |
| Security Incident (Sentinel)        | -100.00%             |
| NSG Inbound Malicious Flows Allowed | -99.58%              |


