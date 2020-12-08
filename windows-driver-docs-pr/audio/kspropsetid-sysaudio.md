---
title: KSPROPSETID \_ Sysaudio
description: KSPROPSETID \_ Sysaudio
keywords:
- KSPROPSETID_Sysaudio
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2aaa605f02f357386fa2db7277130f8d3967ea7d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801067"
---
# <a name="kspropsetid_sysaudio"></a>KSPROPSETID \_ Sysaudio


## <span id="ddk_kspropsetid_sysaudio_ks"></span><span id="DDK_KSPROPSETID_SYSAUDIO_KS"></span>


`KSPROPSETID_Sysaudio`属性集用于访问[SysAudio 系统驱动程序](./kernel-mode-wdm-audio-components.md#sysaudio-system-driver)的属性。 Sysaudio 是代表 DirectSound 和其他客户端创建和管理 [虚拟音频设备](./virtual-audio-devices.md) 的驱动程序。

SysAudio 的客户端使用此属性集来执行以下操作：

-   枚举 SysAudio 的客户端可用的虚拟音频设备。

-   枚举 SysAudio 能够在虚拟音频设备上实例化的 pin。

-   确定这些针脚的功能。

-   枚举位于流过每个 pin 的数据流路径中的节点。

-   通过 pin 配置数据路径，使其包括或绕过 AEC 节点。

浏览可用虚拟音频设备的属性后，客户端应准备好选择一个虚拟音频设备，并在该设备上创建一个 pin。 某些客户端可能会选择在一个虚拟音频设备上创建多个 pin，或在多个设备上创建 pin。 有关创建 pin 的信息，请参阅 [固定工厂](./pin-factories.md)。

创建 pin 后，客户端可以使用 [KSPROPSETID \_ Sysaudio \_ pin](kspropsetid-sysaudio-pin.md) 属性集来管理 pin。

以下属性是属性集的成员 `KSPROPSETID_Sysaudio` ：

[**KSPROPERTY \_ SYSAUDIO \_ 组件 \_ ID**](ksproperty-sysaudio-component-id.md)

[**KSPROPERTY \_ SYSAUDIO \_ 创建 \_ 虚拟 \_ 源**](ksproperty-sysaudio-create-virtual-source.md)

[**KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 计数**](ksproperty-sysaudio-device-count.md)

[**KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 友好 \_ 名称**](ksproperty-sysaudio-device-friendly-name.md)

[**KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 实例**](ksproperty-sysaudio-device-instance.md)

[**KSPROPERTY \_ SYSAUDIO \_ 设备 \_ 接口 \_ 名称**](ksproperty-sysaudio-device-interface-name.md)

[**KSPROPERTY \_ SYSAUDIO \_ 实例 \_ 信息**](ksproperty-sysaudio-instance-info.md)

[**KSPROPERTY \_ SYSAUDIO \_ 选择 \_ 图**](ksproperty-sysaudio-select-graph.md)

 

