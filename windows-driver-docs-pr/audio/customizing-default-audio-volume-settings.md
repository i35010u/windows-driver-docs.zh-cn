---
title: 自定义 HD 音频驱动程序音量设置
description: 能够自定义 box 高清音频默认音频音量和麦克风提升级别以适应特定 PC，为 Oem 提供其音频适配器安装参数的灵活性。
ms.assetid: 0C86C869-447E-4A77-A723-5D9A17D95C7C
keywords:
- 音频音量设置
- 音频适配器 WDK，音量设置
- 适配器驱动程序 WDK 音频，音量设置
- 自定义音频音量设置
- 端口类音频适配器 WDK，音量设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f951ced9ee5720aa9dd81677e02fa9653b79c5b8
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925618"
---
# <a name="customizing-hd-audio-driver-volume-settings"></a>自定义 HD 音频驱动程序音量设置


能够自定义 box 高清音频默认音频音量和麦克风提升级别以适应特定 PC，为 Oem 提供其音频适配器安装参数的灵活性。

**请注意**  ，仅当使用默认的 Microsoft HD 音频驱动程序时，才可以使用此处所述的过程。

 

默认情况下，HD Audio 类函数驱动程序在预定值处设置音频音量和麦克风提升级别，以确保用户体验到 "开箱即用" 体验。

高清音频类函数驱动程序现在应称为音频类驱动程序，它使用了不同的硬编码默认值，这些默认值不能为任何特定 PC 自定义。 因此，Oem 无法覆盖这些值来满足自身的要求。 要调整的最重要设置之一是卷级别，因为用户对其音频系统的响度或 quietness （尤其是在首次使用时）敏感。

音频类驱动程序已重新设计，以允许您重写硬编码的默认值。 重写音频类驱动程序的硬编码值的机制涉及到编写一个 INF 文件，用于包装音频类驱动程序的收件箱 INF 文件（hdaudio），并使用此包装器 INF 来指定所需的值。

下图显示了一个示例 HD 音频编解码器拓扑。 请注意，存在各个节点的 Id 以及 pin 组合的 Id。![显示表示物理连接器的 pin 组合的示例音频编解码器拓扑。 mic 和 line 输入节点以及扬声器输出节点显示固定复数 id。](images/pin-complexid2.png)

Pin 组合表示相关设备的物理连接器（例如发言人、mic 或 line）。

若要指定自定义音频音量级别或麦克风提升级别，请使用包装 INF 文件来指定每个 pin 复数 ID 的自定义级别。 这些级别表示为 Dword，表示类驱动程序应返回的默认内核流式处理（KS）分贝级别。

当高质音频类驱动程序接收到 KSPROPERTY\_音频\_VOLUMELEVEL 的 GET 请求时，驱动程序将确定注册表中是否存在包含接收到请求的节点的默认卷（或 Mic 提升）值。 如果注册表中存在值，但没有以前缓存的值，则注册表中的默认值将应用于该设备，并且还会在 KSPROPERTY\_AUDIO\_VOLUMELEVEL 响应中返回。 如果注册表中没有任何值，则 HD Audio 类驱动程序将从子设备图形实现中检索默认值。

从 Windows Vista 开始，默认值如下所示：

-   对于所有设备类型，终结点卷默认为最大减 6 dB。

-   麦克风提升默认值为 0 dB。

以下步骤汇总了由音频类驱动程序用来确定要返回的默认值以响应 KSPROPERTY\_音频\_VOLUMELEVEL 的 GET 请求时所使用的算法：

1. 确定包含查询的卷节点的路径终止的固定复数。

2. 执行注册表查找，查看是否已为步骤1中找到的 pin 复杂的卷或麦克风提升默认值。

3. 如果在注册表中找到了值，则驱动程序会将该值设置为最小值（如果该值低于放大器支持的最小值）。 否则，如果该值高于放大器支持的最大值，则将该值设置为最大值。 如果在注册表中找到的值位于放大器支持的范围内，则返回值以响应 GET 请求。 此外，当呈现为复杂的 pin 或从其捕获时，驱动程序会用此值来计划关联的 HD 音频放大器小组件。

以下文件夹树显示了用于保存默认值的驱动程序实例键的布局。

&lt;驱动程序&gt;密钥 DefaultVolumeLevels Pin 复杂（2位十六进制，不带有 "0x"）卷（ks db 步骤中的 dword 步骤）提升（ks db 步骤中的 dword）

KS DB 步进值的定义如下：-2147483648 为-无限大分贝（衰减）

-2147483647 为-32767.99998474 分贝（衰减）

+ 2147483647 为 + 32767.99998474 分贝（增益）

有关所使用的度量单位（1/65536 dB）的详细信息，请参阅[**\_KSPROPERTY AUDIO\_VOLUMELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)。

若要重写 wdmudio 文件，请使用 "包括" 和 "需要" 指令，如[Windows 驱动程序工具包（WDK）8.1 示例](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/master/Official%20Windows%20Driver%20Kit%20Sample/Windows%20Driver%20Kit%20(WDK)%208.1%20Samples)的一部分提供的*Microsoft 虚拟音频设备驱动程序示例*中所示。

```inf
;Copyright (c) Microsoft Corporation. All rights reserved.
;
...
[MSVAD_Simple.NT]
Include=ks.inf,wdmaudio.inf
Needs=KS.Registration, WDMAUDIO.Registration
...
```

有关 Include 和需求指令的详细信息，请参阅[**Inf DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)和[Inf 文件的源媒体](https://docs.microsoft.com/windows-hardware/drivers/install/source-media-for-inf-files)。

下面是一个示例 INF 包装程序，用于包装音频类驱动程序的 INF 文件。

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

由于指定了 HKR 相对路径，因此将根据使用的特定 INF 文件部分确定确切的驱动程序注册表路径。 有关 HKR 相对路径的详细信息，请参阅[**INF AddReg 指令（Windows 驱动程序）**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)。 以下两个注册表路径为示例，你的注册表路径可能会有所不同。

HKEY\_本地\_计算机\\系统\\CurrentControlSet\\控件\\类\\{4d36e96c-e325-11ce-bfc1-08002be10318}\\0002

- 或 -

HKEY\_本地\_计算机\\系统\\CurrentControlSet\\控件\\类\\{4d36e96c-e325-11ce-bfc1-08002be10318}\\0002\\DeviceInterfaces\\eAuxIn

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[默认的音频音量设置](default-audio-volume-settings.md)  
[**KSPROPERTY\_音频\_VOLUMELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)  



