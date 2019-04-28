---
title: 修改的适用于 MSVAD Micarray 的 INF
description: 修改的适用于 MSVAD Micarray 的 INF
ms.assetid: 0bb57f16-3b32-45c8-aca1-4dc96cb7a744
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 623dc4f149a917f657b58fc35008a670628858fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332299"
---
# <a name="modified-inf-for-msvad-micarray"></a>修改的适用于 MSVAD Micarray 的 INF


本主题说明如何修改 Micarray.inf 示例文件，以提供有关如何安装示例的麦克风阵列中所述的安装程序信息[麦克风阵列 Geometry 属性](microphone-array-geometry-property.md)。

导航到 Src\\音频\\Msvad 查找 Micarray.inf。 制作一份原始文件以新名称，然后按如下所示编辑 Micarray.inf:

```inf
// Modified micarray.inf file tailored for a microphone array
[Version]
Signature="$CHICAGO$"
Class=MEDIA
Provider=%MSFT%
ClassGUID={4d36e96c-e325-11ce-bfc1-08002be10318}
DriverVer = 02/22/2007, 6.0.6000.1
CatalogFile=msvad.cat

[SourceDisksNames]
222="MSVAD Driver Disk","",222

[SourceDisksFiles]
vadarray.sys=222

;;This syntax is only recognized on Windows XP and later versions of Windows- it is needed to install 64-bit drivers on
;;Windows Server 2003 with Service Pack 1 (SP1) and later versions of Windows Server.

[Manufacturer]
%MfgName%=MicrosoftDS,NTAMD64,NTIA64

;;  For Windows Server 2003 Service Pack 1 (SP1) and later versions of Windows, a 64-bit OS will not install a driver
;;  unless the Manufacturer and Models Sections explicitly show it is a driver for that platform
;;  But the individual model section decorations (or lack thereof) work as they always have.
;;  All of the model sections referred to are undecorated or NT-decorated, hence work on all platforms

[MicrosoftDS]
%MSVAD_MicArray.DeviceDesc%=MSVAD_MicArray,*MSVADMicArray

;; This section enables you to install on x64-based systems

[MicrosoftDS.NTAMD64]
%MSVAD_MicArray.DeviceDesc%=MSVAD_MicArray,*MSVADMicArray

;;  This section enables you to install on Itanium-based systems

[MicrosoftDS.NTIA64]
%MSVAD_MicArray.DeviceDesc%=MSVAD_MicArray,*MSVADMicArray

[DestinationDirs]
MSVAD_MicArray.CopyList=10,system32\drivers

;======================================================
; MSVAD_MICARRAY
;======================================================
[MSVAD_MicArray]
AlsoInstall=ks.registration(ks.inf),wdmaudio.registration(wdmaudio.inf)
CopyFiles=MSVAD_MicArray.CopyList
AddReg=MSVAD_MicArray.AddReg

[MSVAD_MicArray.CopyList]
vadarray.sys

[MSVAD_MicArray.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Wave%,MSVAD.I.Wave
AddInterface=%KSCATEGORY_CAPTURE%,%KSNAME_Wave%,MSVAD.I.Wave
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Topology%,MSVAD.I.Topo

[MSVAD_MicArray.AddReg]
HKR,,AssociatedFilters,,"wdmaud,swmidi,redbook"
HKR,,Driver,,vadarray.sys

HKR,Drivers,SubClasses,,"wave,midi,mixer"

HKR,Drivers\wave\wdmaud.drv,Driver,,wdmaud.drv
HKR,Drivers\midi\wdmaud.drv,Driver,,wdmaud.drv
HKR,Drivers\mixer\wdmaud.drv,Driver,,wdmaud.drv

HKR,Drivers\wave\wdmaud.drv,Description,,%MSVAD_MicArray.DeviceDesc%
HKR,Drivers\midi\wdmaud.drv,Description,,%MSVAD_MIDI%
HKR,Drivers\mixer\wdmaud.drv,Description,,%MSVAD_MicArray.DeviceDesc%

;======================================================
; COMMON
;======================================================
[MSVAD.I.Wave]
AddReg=MSVAD.I.Wave.AddReg
[MSVAD.I.Wave.AddReg]
HKR,,CLSID,,%Proxy.CLSID%
HKR,,FriendlyName,,%MSVAD.Wave.szPname%

[MSVAD.I.Topo]
AddReg=MSVAD.I.Topo.AddReg
[MSVAD.I.Topo.AddReg]
HKR,,CLSID,,%Proxy.CLSID%
HKR,,FriendlyName,,%MSVAD.Topo.szPname%

;======================================================
; MSVAD_MICARRAY
;======================================================
[MSVAD_MicArray.NT]
Include=ks.inf,wdmaudio.inf
Needs=KS.Registration, WDMAUDIO.Registration
CopyFiles=MSVAD_MicArray.CopyList
AddReg=MSVAD_MicArray.AddReg

[MSVAD_MicArray.NT.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Wave%,MSVAD.I.Wave
AddInterface=%KSCATEGORY_CAPTURE%,%KSNAME_Wave%,MSVAD.I.Wave
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Topology%,MSVAD.I.Topo

[MSVAD_MicArray.NT.Services]
AddService=msvad_micarray,0x00000002,msvad_MicArray_Service_Inst

[msvad_MicArray_Service_Inst]
DisplayName=%msvad_micarray.SvcDesc%
ServiceType=1
StartType=3
ErrorControl=1
ServiceBinary=%10%\system32\drivers\vadArray.sys

;======================================================
; COMMON
;======================================================
[Strings]
MSFT="Microsoft"
MfgName="Microsoft Audio DDK"
MSVAD_MicArray.DeviceDesc="Sample Virtual Audio Device (Mic Array) (WDM)"

MSVAD.Wave.szPname="MSVAD Wave"
MSVAD.Topo.szPname="MSVAD Topology"
MSVAD_MIDI="MSVAD -> WDM Midi Device"

Proxy.CLSID="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
KSCATEGORY_AUDIO="{6994AD04-93EF-11D0-A3CC-00A0C9223196}"
KSCATEGORY_RENDER="{65E8773E-8F56-11D0-A3B9-00A0C9223196}"
KSCATEGORY_CAPTURE="{65E8773D-8F56-11D0-A3B9-00A0C9223196}"

KSNAME_Wave="Wave"
KSNAME_Topology="Topology"

msvad_micarray.SvcDesc="Sample Virtual Audio Device (Mic Array) (WDM)"

MediaCategories="SYSTEM\CurrentControlSet\Control\MediaCategories"
Simple.NameGuid="{946A7B1A-EBBC-422a-A81F-F07C8D40D3B4}"
Simple.Name="MSVAD (Simple)"
```

在前面的示例所示修改文件后，将其保存在其原始位置。 有关如何生成麦克风数组示例驱动程序的详细信息，请参阅[麦克风阵列 Geometry 属性](microphone-array-geometry-property.md)。

 

 




