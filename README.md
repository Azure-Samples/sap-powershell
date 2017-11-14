[sap-ha-file-share-installation]:https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/sap-high-availability-installation-wsfc-file-share

# SAP PowerShell Scripts

The PowerShell scrips located in [SAPScripts.psm1](https://github.com/goraco/sap-powershell/blob/master/SAPScripts.psm1) file, contains command lets for updating SAP profiles.  

This is needed when you configure SAP high availability on Microsoft Failover Cluster using file share, as documented in [SAP NetWeaver HA Installation on Windows Failover Cluster and File Share for SAP (A)SCS Instance on Azure][sap-ha-file-share-installation]

## Features

PowerShell command-let  **Update-SAPASCSSCSProfile**,  updates SAP ABAP ASCS or SAP Java SCS profile as well as DEFAULT.PFL to new ASCS/SCS  hostname and new GLOBALHOST name.


## Getting Started

### Installation

Import PowerShell module:

```PowerShell
Import-Module C:\tmp\SAPScripts.psm1
 ```
### SYNTAX

```PowerShell
Update-SAPASCSSCSProfile [-PathToAscsScsInstanceProfile] <String> [-NewASCSHostName] <String> [-NewSAPGlobalHostName] <String> [<CommonParameters>]
 ```

### DESCRIPTION

Update-SAPASCSSCSProfile updates SAP ABAP ASCS or SAP Java SCS profile as well as DEFAULT.PFL to new ASCS/SCS hostname and new GLOBALHOST name.

You can specify path to original ASCS/SCS profile file using local or UNC path. From the profile name will be read old ASCS / SCS hostname.

If you specify local path, ASCS/SCS profile parameters are set to use local path. In this case clustered SAP ASCS/SCS instance and SOFS (Scale Out File Server) are runnign on the SAME cluster.

Similary, if you specify UNC path ACS/SCS profile parameters are set to use UNC path. In this case clustered SAP ASCS/SCS instance and SOFS (Scale Out File Server) are runnign on DIFFERENT clusters.


### EXAMPLE

Execute _Update-SAPASCSSCSProfile_ command-let:

```PowerShell
Update-SAPASCSSCSProfile -PathToAscsScsInstanceProfile C:\usr\sap\SF1\SYS\profile\SF1_ASCS00_sf1-sofs1
 ```

 Update SAP Java SCS instance to new  SCS host 'ja1scs', and new GLOBALHOST 'ja1global'. SOFS is reached using
 'ja1global' hostname. SAP SCS instance and SOFS are runnign on DIFFERENT clusters.

 SAP SCS instance is configured to access SAP GLOBALHOST using UNC file share path e.g.
 \\\\ja1global\sapmnt\JA1\SYS\....
