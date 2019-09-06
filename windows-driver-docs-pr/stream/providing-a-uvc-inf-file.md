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
ms.openlocfilehash: daee1d82ff9f64741fcb92a843e3bc900c2f8ae4
ms.sourcegitcommit: 48c4b6d3a504583d2f588ed892a4a281d4b58301
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2019
ms.locfileid: "70387068"
---
# <a name="providing-a-uvc-inf-file"></a>提供 UVC INF 文件

本部分说明设备特定 INF 文件的各个部分。

此类 INF 文件可用于提供设备特定的名称或注册扩展插件单元。

通常，提供安装包的供应商可以使用安装包注册插件 DLL，在这种情况下，供应商不提供 INF 文件。 对于驱动程序签名，提供安装包（而不是特定于设备的 INF 文件）可能更容易。

但请注意，必须使用 INF 文件安装此特定示例。

为此，请将以下代码包含在 INF 文件中，并将其任意命名为*Xuplgin*：

```INF
; Copyright (c) CompanyName. All rights reserved.

[Version]
Signature="$Windows NT$"
Class=Image
ClassGUID={6bdd1fc6-810f-11d0-bec7-08002be2092f}
Provider=%CompanyName%

[SourceDisksNames]
1=%Package%

[SourceDisksFiles]
MyPlugin.ax=1

[ControlFlags]
ExcludeFromSelect=*

[DestinationDirs]
MyDevice.CopyList=11    ; %systemroot%\system32 on NT-based systems

[Manufacturer]
%CompanyName%=CompanyName,NT$ARCH$
```

设备特定的 INF 文件与基于 VID/PID 标识符的设备匹配。 在这种情况下，特定于设备的 INF 文件优先于*Usbvideo*。

```INF
[CompanyName.NT$ARCH$]
%MyDevice.DeviceDesc%=MyDevice,USB\Vid_XXXX&Pid_XXXX&MI_XX

[MyDevice]
Include=usbvideo.inf, ks.inf, kscaptur.inf, dshowext.inf
Needs=USBVideo.NT, KS.Registration, KSCAPTUR.Registration.NT, DSHOWEXT.Registration
AddReg=MyDevice.Plugins
CopyFiles=MyDevice.CopyList
```

INF 还需要 CopyFiles 部分，将插件复制到系统文件夹。
```INF
[MyDevice.CopyList]
MyPlugin.ax
```

以下 INF AddReg 部分的第一部分将注册该插件。  此部分的剩余部分显示基于节点的扩展单元插件的注册表项。 有关类似示例，请参阅*Usbvideo。*

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

以下 INF 部分显示了如何填充特定于接口的注册表项。

```INF
[MyDevice.Interfaces]
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

对于 USB 摄像机，如果设备接口注册表项的位置包含的 DWORD 注册表项**EnableDependentStillPinCapture**的值为非零值，则会将此类相机上的相关 pin 用于照片捕获。 如果注册表项不存在或设置为零，则不会使用该依赖 pin。 相反，照片捕获将使用从预览 pin 拍摄的帧完成。  以下内容启用依赖静止 pin 捕获：

```INF
HKR,,EnableDependentStillPinCapture,0x00010001,1
```

还可以定义一个名为**UvcFlags**的可选注册表值。 **UvcFlags**应为 DWORD 值。 设备接通电源时，UVC 驱动程序将收到即插即用（PnP）启动请求。 然后，驱动程序会在设备注册表项中搜索**UvcFlags** 。 DWORD 值是一个位掩码，可以包含下表中的值。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>位掩码名称</strong></p></td>
<td><p><strong>ReplTest1</strong></p></td>
<td><p><strong>说明</strong></p></td>
</tr>
<tr class="even">
<td><p>WORKAROUNDS_DV_INTERLEAVED_DEFAULT_MASK</p></td>
<td><p>0x00000001</p></td>
<td><p>UVC 支持仅视频数据范围和交错 DV 数据范围。 为交错 DV 设置此位掩码。</p></td>
</tr>
<tr class="odd">
<td><p>WORKAROUNDS_SUPPRESS_CLOCK_MASK</p></td>
<td><p>0x00000002</p></td>
<td><p>当前未使用。</p></td>
</tr>
<tr class="even">
<td><p>WORKAROUNDS_MPEG2TS_SUPPORT_FID</p></td>
<td><p>0x00000004</p></td>
<td><p>FID 掩码指示 stream 标头包含 FID 位。</p></td>
</tr>
<tr class="odd">
<td><p>WORKAROUNDS_MPEG2TS_SUPPORT_EOF</p></td>
<td><p>0x00000008</p></td>
<td><p>EOF 掩码指示负载标头包含帧尾位。</p></td>
</tr>
<tr class="even">
<td><p>WORKAROUNDS_VARIABLE_FRAME_RATE_MASK</p></td>
<td><p>0x00000010</p></td>
<td><p>如果设备可能会改变帧速率，请设置此掩码。 固定速率 DV 设备不应设置此掩码。</p></td>
</tr>
</tbody>
</table>

 

包括类似于以下示例的行，以指定要应用的位掩码：

```INF
HKR,,UvcFlags,0x00010001,0x00000010
```

如果在 Windows Server 2003 和 Windows Vista 或更高版本的操作系统上使用 UVC 驱动程序，则可以将 FID 和 EOF 掩码与基于流的格式（如 MPEG-2 TS）结合使用。

在较低的帧速率条件下，EOF 位的报告完成速度可能比下帧的 FID 位更快。 EOF 位可用于减少在传递 MPEG-2 帧时的延迟。

有关 AddReg 指令的位置语法的详细信息，请参阅[**INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)。

最后一节提供缺少 INF 的定义。

```INF
[Strings]
; Non-localizable
Plugin.CLSID="{zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz}"
ProxyVCap.CLSID="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
XU_GUID="{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
KSCATEGORY_RENDER="{65E8773E-8F56-11D0-A3B9-00A0C9223196}"
KSCATEGORY_CAPTURE="{65E8773D-8F56-11D0-A3B9-00A0C9223196}"
KSCATEGORY_VIDEO="{6994AD05-93EF-11D0-A3CC-00A0C9223196}"

; Localizable
CompanyName="CompanyName"
Package="Installation Package"
MyDevice.DeviceDesc="CompanyName Camera"

PlugIn_IMyExtensionUnit="CompanyName Extension Unit Interface"
```
