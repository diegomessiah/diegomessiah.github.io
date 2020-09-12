---
layout: single
title: "Explained : Get List of devices connected to Mailbox (Office 365)"
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
**Test environment** Powershell v.5
{% endcapture %}
{{mynote}}{: .notice--info}

## Script to get List of devices connected to Mailbox (Office 365) explained

This script returns all the Exchange ActiveSync mobile devices that are users has used that are associated with their mailboxes.

Link : <a href="https://github.com/diegomessiah/Office_365/blob/master/Device_List_Mobile.ps1" target="_blank">My Office 365 Repository</a>

Author:   <a href="https://github.com/diegomessiah" target="_blank">Diego Messiah</a>

First Part - Connection to the Tenant
```
 $credentials = Get-Credential -Credential Admin@ACME.com
 Write-Output "Getting the Exchange Online cmdlets"
    $session = New-PSSession -ConnectionUri https://outlook.office365.com/powershell-liveid/ `
        -ConfigurationName Microsoft.Exchange -Credential $credentials `
        -Authentication Basic -AllowRedirection
    Import-PSSession $session
```
Second Part - Setup Variable and CSV.
```
#Location of CSV
$csv = ".\MobileDevices.csv" 
$results = @()
#The default quota is for 1000 items
$mailboxUsers = get-mailbox -resultsize unlimited
$mobileDevice = @()
```

Third Part - Get the information

We get relevant information like UPN (User ID or User Principal Name), Type of program, First Sync Time (Date and hour of the mailbox first sync)


```
foreach($user in $mailboxUsers)
{
$UPN = $user.UserPrincipalName
#Get-MobileDevice
$mobileDevices = Get-MobileDevice -Mailbox $UPN

      foreach($mobileDevice in $mobileDevices)
      {
          Write-Output "Getting info about a device for $user"
          $properties = @{
          Name = $user.name
          UserDisplayName = $mobileDevice.UserDisplayName
          UPN = $UPN
          ClientType = $mobileDevice.ClientType
          DeviceModel = $mobileDevice.DeviceModel
          DeviceOS = $mobileDevice.DeviceOS
          DeviceTelephoneNumber = $mobileDevice.DeviceTelephoneNumber
          FirstSyncTime = $mobileDevice.FirstSyncTime
          IsValid = $mobileDevice.IsValid
          ExchangeObjectId = $mobileDevice.ExchangeObjectId 
          IsManaged = $mobileDevice.IsManaged
          IsCompliant = $mobileDevice.IsCompliant
          IsDisabled = $mobileDevice.IsDisabled
          }
          $results += New-Object psobject -Property $properties
      }
}
```
Fourth Part - Order the info
```
$results | Select-Object Name,UserDisplayName,UPN,ClientType,DeviceModel,DeviceOS,DeviceTelephoneNumber,FirstSyncTime,IsValid,ExchangeObjectId,IsManaged,IsCompliant,IsDisabledName | Export-Csv -notypeinformation -Path $csv
```
And last but not least - Close the connection
```
Remove-PSSession $session
```
The complete script is in <a href="https://github.com/diegomessiah/Office_365/blob/master/Device_List_Mobile.ps1" target="_blank">My Office 365 Repository</a>
