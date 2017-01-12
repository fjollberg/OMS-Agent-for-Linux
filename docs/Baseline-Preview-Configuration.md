# Configuration for Security Baseline data collection and assessment (Preview)

1. Download the OMS Agent for Linux, version 1.2.0-148 or above:  
	* [OMS Agent for Linux GA v1.2.0-148](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/tag/OMSAgent-201610-v1.2.0-148)    
    * Only 64 bits version is supported in this preview.

2. Install and configure the agent as described here:  
    * [Documentation for OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux)  
  
3. Download the Baseline Preview installation file and untar it on OMS Agent machine:
    * [BaselinePreview.tar.gz](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/baseline-preview/docs/BaselinePreview.tar.gz)    

4. Place the files from BaselinePreview.tar.gz on the OMS Agent machine:  
	* security_baseline.conf  
	_Fluentd configuration file to enable collection and assessment Security Baseline_  
	Destination path on Agent machine: ```/etc/opt/microsoft/omsagent/conf/omsagent.d/```  
    
	* oms_audits.xml  
	_Security Baseline Assessment Rules collection_  
	Destination path on Agent machine: ```/etc/opt/microsoft/omsagent/conf/omsagent.d/```  

	* filter_security_baseline.rb  
	_Fluentd Security Baseline filter plugin_  
	Destination path on Agent machine: ```/opt/microsoft/omsagent/plugin/```  

	* security_baseline_lib.rb  
	_Main Security Baseline implementation library_  
	Destination path on Agent machine: ```/opt/microsoft/omsagent/plugin/```  

	* omsbaseline  
	_Security Baseline tool for collection and assessment data_  
	Destination path on Agent machine: ```/opt/microsoft/omsagent/plugin/```  
    Destination file permissions: ```755```  
    
5. Restart the OMS agent:  
```sudo service omsagent restart``` or ```systemctl restart omsagent```

6. Confirm that there are no errors in the OMS Agent log:  
```tail /var/opt/microsoft/omsagent/log/omsagent.log```
    One minute after restart the OMS agent, the following line should apear in the log:
```[info]: Security Baseline Summary: {"DataType"=>"SECURITY_BASELINE_SUMMARY_BLOB", "IPName"=>"Security", "DataItems"=>[{"Computer"=>"OMS-LinuxBaseline", "TotalAssessedRules"=>78, "CriticalFailedRules"=>0, "WarningFailedRules"=>1, "InformationalFailedRules"=>1, "PercentageOfPassedRules"=>97, "AssessmentId"=>"3b0373f5-835e-4758-a2eb-fb8a2068f5e9", "OSName"=>"Linux", "BaselineType"=>"Linux"}]}```

7. The Security Baseline Summary assessment results will appear in OMS under the **SecurityBaseline** or ***SecurityBaselineSummary** types.  
Log search queries: ```Type=SecurityBaseline``` or ```Type=SecurityBaselineSummary```
