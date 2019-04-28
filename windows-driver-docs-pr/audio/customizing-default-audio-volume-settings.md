---
title: 自定义 HD 音频驱动程序音量设置
description: 可以自定义箱 HD 音频默认音频音量和麦克风提升级别以满足特定的 PC，为 Oem 提供了其音频适配器中某些灵活性安装参数。
ms.assetid: 0C86C869-447E-4A77-A723-5D9A17D95C7C
keywords:
- 音频的音量设置
- 音频适配器 WDK、 音量设置
- 适配器驱动程序 WDK 音频音量设置
- 自定义音频音量设置
- 端口类音频适配器 WDK、 音量设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f5ba4155d7a499646fadbee71b166d7c816f441
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333838"
---
# <a name="customizing-hd-audio-driver-volume-settings"></a>自定义 HD 音频驱动程序音量设置


可以自定义箱 HD 音频默认音频音量和麦克风提升级别以满足特定的 PC，为 Oem 提供了其音频适配器中某些灵活性安装参数。

**请注意**  如果使用默认 Microsoft HD Audio 驱动程序，则只能使用此处所述的过程。

 

默认情况下，HD Audio 类功能驱动程序设置音频的音量和麦克风提升级别在预先确定的值，以确保愉快的"现成"体验的用户。

HD Audio 类功能驱动程序，我现在应称为音频类驱动程序，使用各种不能自定义适用于任何特定的 PC 的硬编码默认值。 在这种情况下，Oem 不能重写这些值以满足其自己的要求。 其中一个最重要的设置来调整音量级别、 用户以及响度或其音频系统 quietness 敏感，尤其是在首次使用。

经过重新设计的音频类驱动程序，以允许你重写的硬编码默认值。 重写音频类驱动程序的硬编码值的机制涉及编写包装的音频类驱动程序的收件箱 INF 文件 (hdaudio.inf) 的 INF 文件和使用此包装 INF 指定所需的值。

下图显示示例 HD Audio 编解码器拓扑。 请注意，有的各个节点的 Id，以及 pin 组合的 Id。![显示表示物理连接器的 pin 组合的音频编解码器拓扑的示例。 mic 和行输入节点，和演讲者输出节点显示 pin 复杂 id。](images/pin-complexid2.png)

Pin 组合表示物理连接器，以获取关联的设备 （例如演讲者、 mic 或行）。

若要指定自定义音频音量级别或麦克风提升级别，请使用该包装器 INF 文件以指定每个自定义级别，将固定复杂的 id。 级别表示为表示流式处理 (KS) 级分贝级别类驱动程序应返回的默认内核的 dword 值。

当 HD Audio 类驱动程序收到的 GET 请求的 KSPROPERTY\_音频\_VOLUMELEVEL，驱动程序确定是否有默认卷 （或 Mic boost） 中包含接收到的节点的路径的注册表值该请求。 如果在注册表中，一个值，但没有以前缓存的值，将应用到设备，并在 KSPROPERTY 中还返回在注册表中的默认值\_音频\_VOLUMELEVEL 响应。 如果在注册表中没有任何值，HD Audio 类驱动程序从子设备图形实现检索默认值。

从 Windows Vista 开始，默认值如下所示：

-   终结点的卷将默认为最大值减去 6 dB 为所有设备类型。

-   麦克风 boost 默认值为 0 的 dB。

以下步骤总结了音频类驱动程序用于确定要为 KSPROPERTY 以响应 GET 请求返回的默认值的算法\_音频\_VOLUMELEVEL:

1. 确定复杂 pin 包含查询的卷节点的路径会终止。

2. 执行注册表查找，以查看针对复杂 pin 找到在步骤 1 中提供了卷或麦克风提升默认值。

3. 如果在注册表中发现的值，然后该驱动程序将该值设置为最小值，如果它低于放大器支持的最小值。 否则值设置为最大值，如果它在上面放大器支持的最大值。 如果在注册表中找到的值为放大器所支持的范围内，则以响应 GET 请求返回值。 此外，驱动程序以呈现或捕获从 pin 复杂时此值与关联的 HD Audio 放大器小组件。

下面的文件夹树显示驱动程序实例保存的项的默认值的布局。

&lt;驱动程序键&gt;DefaultVolumeLevels Pin 复杂 （2 位数的十六进制数不以"0x"开头） 卷 (DWORD KS DB 步骤中) 提升 (DWORD KS DB 步骤中)

KS DB 单步执行值定义，如下所示:-2147483648 是-无穷大分贝 （衰减）

在-2147483647 是-32767.99998474 分贝 （衰减）

+2147483647 是 +32767.99998474 分贝 （提升）

在单元上的度量值是使用 (1/65536 dB) 的详细信息，请参阅[ **KSPROPERTY\_音频\_VOLUMELEVEL**](https://msdn.microsoft.com/library/windows/hardware/ff537309)。

若要重写 wdmudio.inf 文件，使用 Include 和需求指令从下面的代码段中所示*Microsoft 虚拟音频设备驱动程序示例*作为的一部分[Windows Driver Kit (WDK) 8.1 示例](https://go.microsoft.com/fwlink/p/?LinkId=618052).

```inf
;Copyright (c) Microsoft Corporation. All rights reserved.
;
...
[MSVAD_Simple.NT]
Include=ks.inf,wdmaudio.inf
Needs=KS.Registration, WDMAUDIO.Registration
...
```

Include 和需求指令的详细信息，请参阅[ **INF DDInstall 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)并[INF 文件的源媒体](https://msdn.microsoft.com/library/windows/hardware/ff552302)。

以下是示例 INF 包装所包装的音频类驱动程序的 INF 文件。

```text
;Copyright (c) Microsoft Corporation. All rights reserved.
;
;Module Name:
;    HDAUDVOL.INF
;
;Abstract:
;    Wrapper INF file for installing the Microsoft UAA Function Driver for High
;    Definition Audio with specific INF overrides

[Version]
Signature="$Windows NT$"
Class=MEDIA
ClassGuid={4d36e96c-e325-11ce-bfc1-08002be10318}
Provider=Microsoft
DriverVer=07/28/2012,6.2.9201.0
CatalogFile=hdaudvol.cat

[Manufacturer]
Microsoft = Microsoft,ntamd64,ntarm

[ControlFlags]
ExcludeFromSelect = *

;;====================================================================================
;; Edit the PNP ID (HDAUDIO\FUNC_01...) below to match the codec + subsystem you are ;; configuring.
;;====================================================================================

[Microsoft]
%HdAudModel_DefaultVolume_DeviceDesc% = HdAudModel_DefaultVolume, HDAUDIO\FUNC_01&VEN_10EC&DEV_0889&SUBSYS_00000000&REV_1000

[Microsoft.ntamd64]
%HdAudModel_DefaultVolume_DeviceDesc% = HdAudModel_DefaultVolume, HDAUDIO\FUNC_01&VEN_10EC&DEV_0889&SUBSYS_00000000&REV_1000

[Microsoft.ntarm]
%HdAudModel_DefaultVolume_DeviceDesc% = HdAudModel_DefaultVolume, HDAUDIO\FUNC_01&VEN_10EC&DEV_0889&SUBSYS_00000000&REV_1000

;;===================== HdAudModel_DefaultVolume ==============================

[HdAudModel_DefaultVolume]
Include=hdaudio.inf
Needs=HDAudModel
AddReg=HdAudModel_DefaultVolume.HdAudInit

[HdAudModel_DefaultVolume.HW]
Include=hdaudio.inf
Needs=HdAudModel.HW

[HdAudModel_DefaultVolume.Services]
Include=hdaudio.inf
Needs=HdAudModel.Services

[HdAudModel_DefaultVolume.Interfaces]
Include=hdaudio.inf
Needs=HdAudModel.Interfaces

[HdAudModel_DefaultVolume.HdAudInit]
;;====================================================================================
;; Units are in KS dB so 1dB == 65536 (0x00010000)
;; ======================================================================================
HKR,DefaultVolumeLevels\18,Volume,1,00,00,FE,FF ; Set to 0xFFFE0000 to set to -2dB
HKR,DefaultVolumeLevels\18,Boost,1,00,00,0A,00 ; Set to 0x000A0000 to set to 10dB

[Strings]
HdAudModel_DefaultVolume_DeviceDesc = "High Definition Audio Device"
```

由于指定 HKR 相对路径，将基于特定的 INF 文件部分，可确定确切驱动程序注册表路径。 有关 HKR 相对路径的详细信息，请参阅[ **INF AddReg 指令 （Windows 驱动程序）**](https://msdn.microsoft.com/library/windows/hardware/ff546320)。 以下两个注册表路径示例，你的注册表路径可能会有所不同。

HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Class\\{4d36e96c-e325-11ce-bfc1-08002be10318}\\0002

- 或 -

HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Class\\{4d36e96c-e325-11ce-bfc1-08002be10318}\\0002\\DeviceInterfaces\\eAuxIn

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[默认音频的音量设置](default-audio-volume-settings.md)  
[**KSPROPERTY\_音频\_VOLUMELEVEL**](https://msdn.microsoft.com/library/windows/hardware/ff537309)  



