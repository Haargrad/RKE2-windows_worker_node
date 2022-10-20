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

New-NetIPAddress -InterfaceAlias Ethernet0 -IPAddress 172.16.1.2 -PrefixLength 24 -DefaultGateway 172.16.1.1

Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0

Set-Service sshd -StartupType Automatic

Set-Service ssh-agent -StartupType Automatic

Start-Service sshd

Start-Service ssh-agent

Invoke-WebRequest -UseBasicParsing "https://raw.githubusercontent.com/microsoft/Windows-Containers/Main/helpful_tools/Install-ContainerdRuntime/install-containerd-runtime.ps1" -o install-containerd-runtime.ps1
.\install-containerd-runtime.ps1
