# WARNING
The EXE file is not accessible now.
After an update I will upload it again.

# Extract SCOM monitoring details
A PowerShell script - translated to an EXE file - that extracts SCOM monitoring details - all running and enabled Management Pack monitoring objects - covering a monitored server chosen by the customer. You can run this application in a CMD as well as in a simple PowerShell window.
The only requirement is that you need to run this script on a SCOM Management Server.

### Remark
This version extracts the monitoring details using the factory default settings, so if an override is defined for a Monitor or Rule then that is not shown. Later I will update the script to contain such information some way.

## The Monitor extract has the following data:
- Monitor DisplayName ⟶ The DisplayName property of the Monitor
- Monitor Name ⟶ The internal Name property of the Monitor (as you can find it in a Management Pack)
- Monitor Description ⟶ The Description field of the Monitor (should be empty)
- MP Name [MP DisplayName] ⟶ The internal Name property, and the DisplayName property in squared brackets of the Management Pack in which the Monitor is defined
- Instance DisplayName ⟶ The DisplayName property of the instance
- Monitor Target DisplayName ⟶ The DisplayName property of the Target of the Monitor
- Generates Alert ⟶ The Monitor generates an Alert (True or False)
- Alert Severity ⟶ If the Monitor generates an Alert then it has this Severity value (Error, Warning, Information, MatchMonitorHealth)
- Alert Priority ⟶ If the Monitor generates an Alert then it has this Priority value (High, Normal, Low)
- Alert Name ⟶ If the Monitor generates an Alert then this is the Name of the Alert
- Alert Description ⟶ If the Monitor generates an Alert then this is the Description of the Alert (with a text, or a parameter from SCOM)
- Health State #1 ⟶ The first Health State definition, as it is recorder in the Management Pack. First its name, then its meaning (e.g. TimerEventRaised -> Success means that in the Management Pack the name of the Health State is TimerEventRaised, and it means a Success Health State)
- Health State #2 ⟶ The second Health State definition, as it is recorded in the Management Pack.
- Monitor Type ⟶ The type of the Monitor (possible values are: UnitMonitor, AggregateRollupMonitor, DependencyRollupMonitor)
- Monitor Type ID ⟶ The type ID of the Monitor Type
- Monitor Effective Configuration ⟶ Variable, detailed information of the Monitor configuration

## The Rule extract has the following data:
- Rule DisplayName ⟶ The DisplayName property of the Rule
- Rule Name ⟶ The internal Name property of the Rule (as you can find it in a Management Pack)
- Rule Description ⟶ The Description field of the Monitor (should be empty)
- MP Name [MP DisplayName] ⟶ The internal Name property, and the DisplayName property in squared brackets of the Management Pack in which the Rule is defined
- Instance DisplayName ⟶ The DisplayName property of the instance
- Rule Target DisplayName ⟶ The DisplayName property of the Target of the Rule
- Rule Category ⟶ The Category property of the Rule (should be Alert, EventCollection, PerformanceCollection, System, etc.)
- Generates Alert ⟶ The Rule generates an Alert (True or False)
- Alert Severity ⟶ If the Rule generates an Alert then it has this Severity value (Error, Warning, Information)
- Alert Priority ⟶ If the Rule generates an Alert then it has this Priority value (High, Normal, Low)
- Alert Name ⟶ If the Rule generates an Alert then this is the Name of the Alert
- Alert Description ⟶ If the Rule generates an Alert then this is the Description of the Alert (with a text, or a parameter from SCOM)
- Rule Effective Configuration ⟶ Variable, detailed information of the Rule configuration

To comfortably use this tool you need to understand SCOM, especially the details of the Management Packs.
The extract shows this information, not the information can be read on the GUI of a SCOM Console.
Nevertheless I try to detail as much information here so you can understand the output file better.

## Further information
Additionally you can see these information in the extract text file (not all is listed that you may see in the output file):
- '$Target/Host/Property[Type="Windows!Microsoft.Windows.Computer"]/NetworkName$' ⟶ This is the name of the computer

You need to know that the word before the exclamation mark and after the quotation mark is a reference to a Management Pack. If you need to know which is that Management Pack you need to open the Management Pack in which this object found, then on the \<References\> section you need to find the proper \<Refernce\> entry.

- '$Target/Host/Property[Type="Windows!Microsoft.Windows.Computer"]/PrincipalName$' ⟶ This is the name of the computer
- '$Target/Host/Property[Type="Windows!Microsoft.Windows.Computer"]/NetbiosComputerName$' ⟶ This is the NetBIOS name of the computer
- '$Target/Property[Type="AD!Microsoft.Windows.Server.AD.Library.DomainControllerRole"]/DomainNamingMaster$' ⟶ This is the computer name of the Domain Naming Master of a Windows Active Directory Domain
- '$Target/Property[Type="AD!Microsoft.Windows.Server.AD.Library.DomainControllerRole"]/InfrastructureMaster$' ⟶ This is the computer name of the Infrastructure Master of a Windows Active Directory Domain
- '$Target/Property[Type="AD!Microsoft.Windows.Server.AD.Library.DomainControllerRole"]/PDCEmulator$' ⟶ This is the computer name of the PDC Emulator of a Windows Active Directory Domain
- '$Target/Property[Type="AD!Microsoft.Windows.Server.AD.Library.DomainControllerRole"]/RIDMaster$' ⟶ This is the computer name of the RID Master of a Windows Active Directory Domain
- '$Target/Property[Type="AD!Microsoft.Windows.Server.AD.Library.DomainControllerRole"]/SchemaMaster$' ⟶ This is the computer name of the Schema Master of a Windows Active Directory Domain
- '$Target/Property[Type="Microsoft.SystemCenter.NTService"]/ServiceName$' ⟶ This is the name of a SCOM service running on the computer
- '$Target/Property[Type="Microsoft.SystemCenter.NTService"]/DisplayName$' ⟶ This is the display name of a SCOM service running on the computer
- '$Target/Property[Type="Windows!Microsoft.Windows.LogicalDevice"]/DeviceID$' ⟶ This is the "DeviceID" field of a Windows Logical Device (typically C:, D:, etc. if a Logical Device is a disk)
- '$Target/Property[Type="WindowsServer!Microsoft.Windows.Server.NetworkAdapter"]/PerfmonInstance$' ⟶ This is the description of the network card
- '$Target/Property[Type="SC!Microsoft.SystemCenter.HealthService"]/Version$' ⟶ This is the current version of the SCOM Agent running on the computer
- '$Target/ManagementGroup/Name$' ⟶ The "Name" property of the Management Group
- '$Target/ManagementGroup/Id$' ⟶ The "Id" property of the Management Group
- ComputerName ⟶ This is typically the name of the computer
- CheckStartupType ⟶ This is a "true" or "false" setting that defines whether to examine the startup type os a service or not
- DiskLabel ⟶ This is typically the label of a Windows disk (C: or whatever the disk label is)
- ServiceName ⟶ This is typically the name of the service running on the computer
- LogName ⟶ This is typically the name of the Windows Event Log
- IntervalSeconds ⟶ This typically contains the value of the repetition time
- Interval ⟶ This typically contains the value of the repetition time
- EventDisplayNumber ⟶ Equals with the "Event ID" of a Windows Event Log entry
- EventNumber ⟶ Equals with the "Event ID" of a Windows Event Log entry
- PublisherName ⟶ Equals with the "Source" of a Windows Event Log entry
- Params/Param[1] ⟶ A Parameter in the related Windows Event Log entry (in this case it is the first parameter, but it can be any other)
- TimerWaitInSeconds ⟶ This typically contains the value for the "Auto Reset Timer"
- SyncTime ⟶ This is typically the synchronization time of the Monitor/Rule, so you can set exactly when the Monitor/Rule run
- AllowProxying ⟶ This is typically an overridable property of the Rule
- ObjectName ⟶ This is typically the name of the object of which has a counter from data is collected in a performance collection rule
- CounterName ⟶ This is typically the name of the counter of which data is collected in a performance collection rule
- AllInstances ⟶ This is typically the "true" or "false" based on whether all instances are selected or not
- InstanceName ⟶ This is typically the name of the instance
- Frequency ⟶ This typically contains the value of the repetition time
- Tolerance ⟶ This is typically the difference number in percentage or value, based on ToleranceType
- ToleranceType ⟶ This defines how to understand the Tolerance, should be "Percentage" or "Absolute"
- MaximumSampleSeparation ⟶ This is typically the maximum number of samples that are NOT collected if they are under the Tolerance
- TimeoutSeconds ⟶ This is typically the timeout (in seconds) for a script. If the script runs longer than this time it is stopped by SCOM Agent.
- NumSamples ⟶ This is typically the number of samples collected which are higher or lower - defined in Direction - than the specified Threshold
- NumOfSamples ⟶ This is typically the number of samples collected
- TargetComputerName ⟶ This is the name of the computer
- Threshold ⟶ This is the reference value against which we compare the samples
- ThresholdError ⟶ This is the reference value against which we compare the samples
- ThresholdWarn ⟶ This is the reference value against which we compare the samples
- WarningThreshold ⟶ This is the reference value against which we compare the samples
- ErrorThreshold ⟶ This is the reference value against which we compare the samples
- Direction ⟶ This defines the comparison (less, greater,lessequal, greaterequal)
- TargetVersion ⟶ This is a version number to which the SCOM compares a version of an Agent or whatever it is configured
- AgentVersion ⟶ This is the current version of a SCOM Agent running on the computer

# Version information
1.0

Initial version. This version contains the default settings for the Monitors and Rules that are enabled for a computer instance or hosted by the computer instance (e.g. for Logical Disks, Network Interfaces, etc.)

# Contact
If you find any issues with the script please send the details to the following email: scom.alf at proton.me
