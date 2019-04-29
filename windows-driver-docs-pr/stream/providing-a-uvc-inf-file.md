---
title: 提供 UVC INF 文件
description: 提供 UVC INF 文件
ms.assetid: 44311eb8-1035-466c-878b-a5d964b34490
keywords:
- INF 文件 WDK USB 视频类
- UVC INF 文件 WDK USB 视频类
- UVC INF 文件 WDK USB 视频类，示例代码
- 示例代码 WDK USB 视频类，UVC INF 文件
ms.date: 09/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 50ff6912c15ae7686a297bed448f8db329176fcd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390876"
---
# <a name="providing-a-uvc-inf-file"></a>提供 UVC INF 文件

本部分说明了特定于设备的 INF 文件的各个部分。

若要提供特定于设备的名称或注册插件扩展单元，可以使用类似如下的 INF 文件。

一般情况下，供应商提供一个安装程序包，可以使用安装包，用例供应商不提供 INF 文件注册插件 DLL。 对于驱动程序签名，它可能更轻松地提供一个安装程序包，而不是特定于设备的 INF 文件。

但应注意，您必须通过使用 INF 文件安装此特定示例。

若要执行此操作，包括下面的代码在 INF 文件中，此处任意名为*Xuplgin.inf*:

```INF
; Copyright (c) CompanyName. All rights reserved.

[Version]
Signature="$CHICAGO$"
Class=Image
ClassGUID={6bdd1fc6-810f-11d0-bec7-08002be2092f}
Provider=%CompanyName%

[SourceDisksNames]
1=%Package%

[SourceDisksFiles.x86]
MyPlugin.ax=1

[ControlFlags]
ExcludeFromSelect=*

[DestinationDirs]
MyDevice.CopyList=11    ; %systemroot%\system32 on 
   NT-based systems

[Manufacturer]
%CompanyName%=CompanyName
```

设备基于 VID/PID 标识符匹配的特定于设备的 INF 文件。 在这种情况下，特定于设备的 INF 文件将优先于*Usbvideo.inf*。

```INF
[CompanyName]
%MyDevice.DeviceDesc%=MyDevice,USB\Vid_XXXX&Pid_XXXX&MI_XX

[MyDevice.NT]
Include=usbvideo.inf, ks.inf, kscaptur.inf, dshowext.inf
Needs=USBVideo.NT, KS.Registration, KSCAPTUR.Registration.NT,
DSHOWEXT.Registration
AddReg=MyDevice.Plugins
CopyFiles=MyDevice.CopyList
```

INF 文件的以下部分显示基于节点的扩展单元的注册表条目插件。 请参阅*Usbvideo.inf*为相似的示例。

```INF
[MyDevice.PlugIns]
HKCR,CLSID\%Plugin.CLSID%,,,%PlugIn_IExtensionUnit%
HKCR,CLSID\%Plugin.CLSID%\InprocServer32,,,MyPlugin.ax
HKCR,CLSID\%Plugin.CLSID%\InprocServer32,ThreadingModel,,Both

; The IID is aggregated onto the node given the GUID of the property set
HKLM,System\CurrentControlSet\Control\NodeInterfaces\%XU_GUID%,,,
   %PlugIn_IExtensionUnit%
; IID in Little-Endian form
HKLM,System\CurrentControlSet\Control\NodeInterfaces\%XU_GUID%,IID,
   1,yy,yy,yy,yy,yy,yy,yy,yy,yy,yy,yy,yy,yy,yy,yy,yy
;CLSID in Little-Endian form
HKLM,System\CurrentControlSet\Control\NodeInterfaces\%XU_GUID%,
   CLSID,1,zz,zz,zz,zz,zz,zz,zz,zz,zz,zz,zz,zz,zz,zz,zz,zz
```

```INF
[MyDevice.NT.Interfaces]
AddInterface=%KSCATEGORY_CAPTURE%,GLOBAL,MyDevice.Interface
AddInterface=%KSCATEGORY_RENDER%,GLOBAL,MyDevice.Interface
AddInterface=%KSCATEGORY_VIDEO%,GLOBAL,MyDevice.Interface

[MyDevice.Interface]
AddReg=MyDevice.Interface.AddReg
 
[MyDevice.Interface.AddReg]
HKR,,CLSID,,%ProxyVCap.CLSID%
HKR,,FriendlyName,,%MyDevice.DeviceDesc%
HKR,,RTCFlags,0x00010001,0x00000010
```

用于 USB 摄像机，如果设备接口注册表项位置中包含的 DWORD 注册表项**EnableDependentStillPinCapture**具有非零值，这种照相机上的依赖 pin 将使用照片拍摄的。 如果注册表项不存在，或者设置为零，将不使用依赖的 pin。 相反，将完成照片拍摄使用从预览针拍摄的帧。

您还可以定义一个可选的注册表值称为**UvcFlags**。 **UvcFlags**应为 DWORD 值。 当在插入设备时，UVC 驱动程序将接收插即用 (PnP) 启动请求。 然后，该驱动程序搜索的**UvcFlags**设备注册表项中。 将 DWORD 值是一个位掩码，并且可以包含下表中的值。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>位掩码名称</strong></p></td>
<td><p><strong>值</strong></p></td>
<td><p><strong>说明</strong></p></td>
</tr>
<tr class="even">
<td><p>WORKAROUNDS_DV_INTERLEAVED_DEFAULT_MASK</p></td>
<td><p>0x00000001</p></td>
<td><p>UVC 支持仅限视频的数据范围和交错的 DV 数据范围。 为交错 DV 设置此位掩码。</p></td>
</tr>
<tr class="odd">
<td><p>WORKAROUNDS_SUPPRESS_CLOCK_MASK</p></td>
<td><p>0x00000002</p></td>
<td><p>当前未使用。</p></td>
</tr>
<tr class="even">
<td><p>WORKAROUNDS_MPEG2TS_SUPPORT_FID</p></td>
<td><p>0x00000004</p></td>
<td><p>FID 屏蔽，指示流标头包含 FID 位。</p></td>
</tr>
<tr class="odd">
<td><p>WORKAROUNDS_MPEG2TS_SUPPORT_EOF</p></td>
<td><p>0x00000008</p></td>
<td><p>EOF 屏蔽，指示负载标头包含结束帧位。</p></td>
</tr>
<tr class="even">
<td><p>WORKAROUNDS_VARIABLE_FRAME_RATE_MASK</p></td>
<td><p>0x00000010</p></td>
<td><p>如果你的设备可能会不同帧速率，请设置此掩码。 固定速率 DV 设备不应设置此掩码。</p></td>
</tr>
</tbody>
</table>

 

包括类似于下面的示例来指定要应用的位掩码的行：

```INF
HKR,,UvcFlags,0x00010001,0x00000010
```

如果在 Windows Server 2003 和 Windows Vista 或更高版本的操作系统上使用 UVC 驱动程序，可以与基于流的格式，如 mpeg-2 TS 使用 FID 和 EOF 掩码。

在较低的帧速率情况下，EOF 位可能会比以下框架的 FID 位更快地报告完成。 EOF 位可用来减少延迟的 mpeg-2 帧传递。

AddReg 指令的位置的语法的详细信息，请参阅[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)。

```INF
[MyDevice.NT.Services]
AddService = usbvideo,0x00000002,MyDevice.ServiceInstall

[MyDevice.ServiceInstall]
DisplayName   = %USBVideo.SvcDesc%
ServiceType   = %SERVICE_KERNEL_DRIVER%
StartType     = %SERVICE_DEMAND_START%
ErrorControl  = %SERVICE_ERROR_NORMAL%
ServiceBinary = %10%\System32\Drivers\usbvideo.sys

[MyDevice.CopyList]
MyPlugin.ax
```

```INF
[Strings]
; Non-localizable
Plugin.CLSID="{zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz}"
ProxyVCap.CLSID="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
XU_GUID="{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
KSCATEGORY_RENDER="{65E8773E-8F56-11D0-A3B9-00A0C9223196}"
KSCATEGORY_CAPTURE="{65E8773D-8F56-11D0-A3B9-00A0C9223196}"
KSCATEGORY_VIDEO="{6994AD05-93EF-11D0-A3CC-00A0C9223196}"
SERVICE_KERNEL_DRIVER=1
SERVICE_DEMAND_START=3
SERVICE_ERROR_NORMAL=1

; Localizable
CompanyName="CompanyName"
Package="Installation Package"
MyDevice.DeviceDesc="CompanyName Camera"
USBVideo.SvcDesc="USB Video Device (WDM)"

PlugIn_IMyExtensionUnit="CompanyName Extension Unit Interface"
```
