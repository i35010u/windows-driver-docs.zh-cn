---
title: 音频驱动程序属性集
description: 音频驱动程序属性集
ms.assetid: bac74ad5-3a9b-40b1-ae49-c86558c34e94
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbd279a2b5bfeec24d975a837d5068c3377f768d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831360"
---
# <a name="audio-drivers-property-sets"></a>音频驱动程序属性集


## <span id="ddk_audio_drivers_property_sets_ks"></span><span id="DDK_AUDIO_DRIVERS_PROPERTY_SETS_KS"></span>


本部分介绍音频特定属性集，这些属性集适用于在 Microsoft Windows 2000 和更高版本以及 Windows Millennium Edition （Me）和 Windows 98 中使用 WDM 内核流式处理服务的音频驱动程序。

每个属性的引用页面都包含一个具有以下列标题的表。


| “获取” | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|-----|-----|--------|--------------------------|---------------------|
|     |     |        |                          |                     |

这些标题具有以下含义：

-   **获取**

    目标 KS 对象是否支持 KSPROPERTY\_类型\_获取属性请求？ （指定 "是" 或 "否"。）

-   **字符集**

    目标 KS 对象是否支持 KSPROPERTY\_类型\_设置属性请求？ （指定 "是" 或 "否"。）

-   **靶**

    请求的目标是将属性请求发送到的 KS 对象。 音频属性的目标是 "筛选器" 或 "pin"。 （属性请求按其内核句柄指定目标对象。）

-   **属性描述符类型**

    属性说明符指定属性和要对该属性执行的操作。 描述符始终以[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))结构开始，但某些类型的描述符包含附加信息。 例如， [**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)结构是以 KSPROPERTY 结构开头但还包含节点 ID 的属性描述符。

-   **属性值类型**

    属性通常具有一个值，并且此值的类型取决于属性。 例如，一个只能处于两种状态的属性（打开或关闭）通常具有 BOOL 值。 可以假设从0到0xFFFFFFFF 的整数值的属性可能有 ULONG 值。 更复杂的属性可能具有作为数组或结构的值。

前面的属性说明符和属性值是在[KS 属性、事件和方法](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties--events--and-methods)中讨论的实例规范和操作数据缓冲区的属性特定版本。

属性请求使用下列标志之一来指定要对属性执行的操作：

-   KSPROPERTY\_类型\_BASICSUPPORT

-   KSPROPERTY\_类型\_GET

-   KSPROPERTY\_类型\_集

所有筛选器和 pin 对象均支持对其属性的基本支持操作。 它们是否支持 get 和 set 操作取决于属性。 表示筛选器或固定对象的固有功能的属性可能只需要 get 操作。 尽管获取操作也可能对读取当前设置很有用，但表示可配置的设置的属性可能只需要设置操作。 有关使用 "获取"、"设置" 和 "基本" 支持操作和音频属性的详细信息，请参阅[音频终结点、属性和事件](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-endpoints--properties-and-events)。

为音频驱动程序定义了以下属性集：

[KSPROPSETID\_E-AC3](kspropsetid-ac3.md)

[KSPROPSETID\_声音\_回音\_取消](kspropsetid-acoustic-echo-cancel.md)

[KSPROPSETID\_音频](kspropsetid-audio.md)

[KSPROPSETID\_AudioEngine](kspropsetid-audioengine.md)

[KSPROPSETID\_AudioGfx](kspropsetid-audiogfx.md)

[KSPROPSETID\_DirectSound3DBuffer](kspropsetid-directsound3dbuffer.md)

[KSPROPSETID\_DirectSound3DListener](kspropsetid-directsound3dlistener.md)

[KSPROPSETID\_DrmAudioStream](kspropsetid-drmaudiostream.md)

[KSPROPSETID\_FMRXTopology](kspropsetid-fmrxtopology.md)

[KSPROPSETID\_Hrtf3d](kspropsetid-hrtf3d.md)

[KSPROPSETID\_Itd3d](kspropsetid-itd3d.md)

[KSPROPSETID\_插座](kspropsetid-jack.md)

[KSPROPSETID\_RTAudio](kspropsetid-rtaudio.md)

[KSPROPSETID\_SoundDetector](kspropsetid-sounddetector.md)

[KSPROPSETID\_合成](kspropsetid-synth.md)

[KSPROPSETID\_SynthClock](kspropsetid-synthclock.md)

[KSPROPSETID\_合成\_Dls](kspropsetid-synth-dls.md)

[KSPROPSETID\_Sysaudio](kspropsetid-sysaudio.md)

[KSPROPSETID\_Sysaudio\_固定](kspropsetid-sysaudio-pin.md)

[KSPROPSETID\_TelephonyControl](kspropsetid-telephonycontrol.md)

[KSPROPSETID\_TelephonyTopology](kspropsetid-telephonytopology.md)

[KSPROPSETID\_TopologyNode](kspropsetid-topologynode.md)

 

 





