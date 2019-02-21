---
title: 音频驱动程序的属性集
description: 音频驱动程序的属性集
ms.assetid: bac74ad5-3a9b-40b1-ae49-c86558c34e94
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 661e29d53d64a01521d0ee891d9f931950ff0ad3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541842"
---
# <a name="audio-drivers-property-sets"></a>音频驱动程序的属性集


## <span id="ddk_audio_drivers_property_sets_ks"></span><span id="DDK_AUDIO_DRIVERS_PROPERTY_SETS_KS"></span>


本部分介绍可用于使用 WDM 内核流式处理服务在 Microsoft Windows 2000 及更高版本的音频驱动程序和 Windows Millennium Edition （me） 和 Windows 98 中的特定于音频的属性集。

每个属性的参考页包含具有以下列标题的表。


| Get | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|-----|-----|--------|--------------------------|---------------------|
|     |     |        |                          |                     |

这些标题具有以下含义：

-   **Get**

    目标 KS 对象是否支持 KSPROPERTY\_类型\_属性的 GET 请求？ （指定是或否）。

-   **Set**

    目标 KS 对象是否支持 KSPROPERTY\_类型\_集属性请求？ （指定是或否）。

-   **Target**

    请求的目标是属性请求发送到 KS 对象。 音频属性的目标是筛选器或 pin。 （属性请求指定的目标对象由其内核句柄。）

-   **属性描述符类型**

    属性描述符指定的属性和要在该属性上执行的操作。 描述符始终开头[ **KSPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff564262)结构，但某些类型的描述符包含其他信息。 例如， [ **KSNODEPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff537143)结构是一个属性说明符开头 KSPROPERTY 结构，但还包括一个节点 id。

-   **属性值类型**

    属性通常具有一个值，并且此值的类型取决于属性。 例如，可以是一个只有两种状态-打开或关闭-中的属性通常具有一个 BOOL 值。 可以假定为 0xFFFFFFFF 0 的整数值的属性可能具有 ULONG 值。 更复杂的属性可能是数组或结构的值。

上述属性描述符和属性值是实例规范和操作数据缓冲区中所述的属性特定于版本[KS 属性、 事件和方法](https://msdn.microsoft.com/library/windows/hardware/ff567673)。

属性请求使用下列标志之一来指定要在属性上执行的操作：

-   KSPROPERTY\_类型\_BASICSUPPORT

-   KSPROPERTY\_TYPE\_GET

-   KSPROPERTY\_TYPE\_SET

所有筛选器和 pin 对象支持属性对其的 basic 支持操作。 是否支持 get 和 set 操作取决于属性。 该属性表示的筛选器或 pin 对象的固有功能是可能需要仅一个 get 操作。 该属性表示可配置的设置可能需要仅设置操作中，尽管可能适用于读取的当前设置的 get 操作。 有关使用具有音频属性的 get、 集和 basic 支持操作的详细信息，请参阅[音频终结点、 属性和事件](https://msdn.microsoft.com/library/windows/hardware/ff536199)。

为音频驱动程序定义以下属性集：

[KSPROPSETID\_AC3](kspropsetid-ac3.md)

[KSPROPSETID\_声学\_Echo\_取消](kspropsetid-acoustic-echo-cancel.md)

[KSPROPSETID\_Audio](kspropsetid-audio.md)

[KSPROPSETID\_AudioEngine](kspropsetid-audioengine.md)

[KSPROPSETID\_AudioGfx](kspropsetid-audiogfx.md)

[KSPROPSETID\_DirectSound3DBuffer](kspropsetid-directsound3dbuffer.md)

[KSPROPSETID\_DirectSound3DListener](kspropsetid-directsound3dlistener.md)

[KSPROPSETID\_DrmAudioStream](kspropsetid-drmaudiostream.md)

[KSPROPSETID\_FMRXTopology](kspropsetid-fmrxtopology.md)

[KSPROPSETID\_Hrtf3d](kspropsetid-hrtf3d.md)

[KSPROPSETID\_Itd3d](kspropsetid-itd3d.md)

[KSPROPSETID\_插孔](kspropsetid-jack.md)

[KSPROPSETID\_RTAudio](kspropsetid-rtaudio.md)

[KSPROPSETID\_SoundDetector](kspropsetid-sounddetector.md)

[KSPROPSETID\_合成器](kspropsetid-synth.md)

[KSPROPSETID\_SynthClock](kspropsetid-synthclock.md)

[KSPROPSETID\_合成器\_Dls](kspropsetid-synth-dls.md)

[KSPROPSETID\_Sysaudio](kspropsetid-sysaudio.md)

[KSPROPSETID\_Sysaudio\_Pin](kspropsetid-sysaudio-pin.md)

[KSPROPSETID\_TelephonyControl](kspropsetid-telephonycontrol.md)

[KSPROPSETID\_TelephonyTopology](kspropsetid-telephonytopology.md)

[KSPROPSETID\_TopologyNode](kspropsetid-topologynode.md)

 

 





