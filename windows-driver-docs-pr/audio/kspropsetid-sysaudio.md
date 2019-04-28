---
title: KSPROPSETID\_Sysaudio
description: KSPROPSETID\_Sysaudio
ms.assetid: 817cbda5-9d37-4c12-8749-98a86540609f
keywords:
- KSPROPSETID_Sysaudio
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bcc6fdd80274d2f73349c292fd11a339d5c2a72
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332453"
---
# <a name="kspropsetidsysaudio"></a>KSPROPSETID\_Sysaudio


## <span id="ddk_kspropsetid_sysaudio_ks"></span><span id="DDK_KSPROPSETID_SYSAUDIO_KS"></span>


`KSPROPSETID_Sysaudio`属性设置用于访问的属性[SysAudio 系统驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff537039#sysaudio-system-driver)。 Sysaudio 是驱动程序，用于创建和管理[虚拟音频设备](https://msdn.microsoft.com/library/windows/hardware/ff538734)代表 DirectSound 和其他客户端。

SysAudio 的客户端使用此属性设置为执行以下操作：

-   枚举 SysAudio 的客户端可用的虚拟音频设备。

-   枚举 SysAudio 是能够实例化的虚拟的音频设备上的球瓶。

-   确定这些引脚的功能。

-   枚举沿着流过每个 pin 的数据流路径的节点。

-   配置通过 pin 以包括或绕过 AEC 节点的数据路径。

浏览可用的虚拟音频设备的属性后, 客户端应准备好选择其中一个虚拟的音频设备，然后在该设备上创建一个 pin。 某些客户端可能会选择虚拟的音频设备上创建多个 pin 或多个设备上创建 pin。 有关创建 pin 信息，请参阅[Pin 工厂](https://msdn.microsoft.com/library/windows/hardware/ff537747)。

创建 pin 后，可以使用客户端[KSPROPSETID\_Sysaudio\_Pin](kspropsetid-sysaudio-pin.md)属性设置为管理 pin。

以下属性属于`KSPROPSETID_Sysaudio`属性集：

[**KSPROPERTY\_SYSAUDIO\_COMPONENT\_ID**](ksproperty-sysaudio-component-id.md)

[**KSPROPERTY\_SYSAUDIO\_CREATE\_VIRTUAL\_SOURCE**](ksproperty-sysaudio-create-virtual-source.md)

[**KSPROPERTY\_SYSAUDIO\_DEVICE\_COUNT**](ksproperty-sysaudio-device-count.md)

[**KSPROPERTY\_SYSAUDIO\_DEVICE\_FRIENDLY\_NAME**](ksproperty-sysaudio-device-friendly-name.md)

[**KSPROPERTY\_SYSAUDIO\_设备\_实例**](ksproperty-sysaudio-device-instance.md)

[**KSPROPERTY\_SYSAUDIO\_DEVICE\_INTERFACE\_NAME**](ksproperty-sysaudio-device-interface-name.md)

[**KSPROPERTY\_SYSAUDIO\_实例\_信息**](ksproperty-sysaudio-instance-info.md)

[**KSPROPERTY\_SYSAUDIO\_SELECT\_GRAPH**](ksproperty-sysaudio-select-graph.md)

 

 





