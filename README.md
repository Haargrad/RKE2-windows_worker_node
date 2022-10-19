# RKE2-windows_worker_node
Create Custom cluster rke2:

network cni calico

defualt all setting 

on windows node:

Set correct time

Enable Hyper-V

DISM /Online /Enable-Feature /All /FeatureName:Microsoft-Hyper-V

Install-WindowsFeature -Name Containers

set-MpPreference -DisableRealtimeMonitoring $true -DisableScriptScanning $true -DisableArchiveScanning $true

stop-process dockerd

stop-service docker

set-service docker -startuptype disabled

