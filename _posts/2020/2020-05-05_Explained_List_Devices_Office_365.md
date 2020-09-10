---
layout: single
title: "Explained : List Devices connected to Office 365 Mailbox"
excerpt: "This article explain how writed script to get list of devices connected to Mailbox (Office 365)"
permalink:
tags:
  - Office 365
  - Explained  
categories:
published: true
comments: true
header:
  teaserlogo:
  teaser: ''
  image: images/headers/mountain01_1920x500.jpg
  caption:
gallery:
  - image_path: ''
    url: ''
    title: ''
toc: true
toc_label: "Table of content"
toc_sticky: true
toc_icon: "terminal"
---

{% capture mynote%}
**Test environment** Python 3.7
{% endcapture %}
{{mynote}}{: .notice--info}

Script to get List of devices connected to Mailbox (Office 365) explained
Link : <a href="https://github.com/diegomessiah/Office_365/blob/master/Device_List_Mobile.ps1" target="_blank">My Office 365 Repository</a>
Author:   <a href="https://github.com/diegomessiah" target="_blank">Diego Messiah</a>

First Part - Connection to the Tenant
'''
 $credentials = Get-Credential -Credential UserAdmin@Company.com
 Write-Output "Getting the Exchange Online cmdlets"
    $session = New-PSSession -ConnectionUri https://outlook.office365.com/powershell-liveid/ `
        -ConfigurationName Microsoft.Exchange -Credential $credentials `
        -Authentication Basic -AllowRedirection
    Import-PSSession $session
'''
Second Part - Setup Variable and CSV
'''
#Location of CSV
$csv = ".\MobileDevices.csv" 
$results = @()
#The default quota is for 1000 items
$mailboxUsers = get-mailbox -resultsize unlimited
$mobileDevice = @()
'''
Third Part - Get the information
'''
foreach($user in $mailboxUsers)
{
$UPN = $user.UserPrincipalName
$displayName = $user.DisplayName

#Get-MobileDevice - https://docs.microsoft.com/en-us/powershell/module/exchange/get-mobiledevice?view=exchange-ps
$mobileDevices = Get-MobileDevice -Mailbox $UPN
       
      foreach($mobileDevice in $mobileDevices)
      {
          Write-Output "Getting info about a device for $displayName"
          $properties = @{
          Name = $user.name
          # User Principal Name 
          UPN = $UPN
          DisplayName = $displayName
          FriendlyName = $mobileDevice.FriendlyName
          ClientType = $mobileDevice.ClientType
          ClientVersion = $mobileDevice.ClientVersion
          DeviceId = $mobileDevice.DeviceId
          DeviceMobileOperator = $mobileDevice.DeviceMobileOperator
          DeviceModel = $mobileDevice.DeviceModel
          DeviceOS = $mobileDevice.DeviceOS
          DeviceTelephoneNumber = $mobileDevice.DeviceTelephoneNumber
          DeviceType = $mobileDevice.DeviceType
          FirstSyncTime = $mobileDevice.FirstSyncTime
          UserDisplayName = $mobileDevice.UserDisplayName
          }
          $results += New-Object psobject -Property $properties
      }
}
'''
Fourth Part - Order the info
'''
$results | Select-Object Name,UPN,FriendlyName,DisplayName,ClientType,ClientVersion,DeviceId,DeviceMobileOperator,DeviceModel,DeviceOS,DeviceTelephoneNumber,DeviceType,FirstSyncTime,UserDisplayName | Export-Csv -notypeinformation -Path $csv
'''
Last Part and not less important - Close the connection
'''
Remove-PSSession $session
'''
The complete script is in <a href="https://github.com/diegomessiah/Office_365/blob/master/Device_List_Mobile.ps1" target="_blank">My Office 365 Repository</a>
