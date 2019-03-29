---
title: 实现硬件卸载的 APO 效果
description: 硬件卸载音频处理对象 (Apo) 的提供可能的性能增强功能，以及电源节省量。
ms.assetid: 159DFFD2-2434-4EDC-A83C-455BA80F74C6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 003ed70c695725b7a1713e910edc8de0835f2c04
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567976"
---
# <a name="implementing-hardware-offloaded-apo-effects"></a>实现硬件卸载的 APO 效果


在 Windows 10 版本 1511年及更高版本，卸载音频处理对象 (Apo) 的支持。 可能的性能增强功能，除了可能的重大节能时有可用使用硬件卸载 a p o s。

两种类型的不可以在硬件卸载播放期间加载。

1. 卸载 Stream 效果 (OSFX)
2. 卸载模式效果 (OMFX)



## <a name="span-idhardwareoffloadedapoeffectsoverviewspanspan-idhardwareoffloadedapoeffectsoverviewspanspan-idhardwareoffloadedapoeffectsoverviewspanhardware-offloaded-apo-effects-overview"></a><span id="Hardware_Offloaded_APO_Effects_Overview"></span><span id="hardware_offloaded_apo_effects_overview"></span><span id="HARDWARE_OFFLOADED_APO_EFFECTS_OVERVIEW"></span>硬件卸载 APO 效果概述


**硬件卸载音频处理和硬件卸载 a p o s**

在 Windows 8 中，音频引擎经过重新设计，使用已卸载到隔离，但连接到计算机的主音频系统的硬件设备的音频流。 这称为硬件卸载。 有关详细信息，请参阅[Hardware-Offloaded 音频处理](hardware-offloaded-audio-processing.md)。

对于需要更大的缓冲区大小的低能耗情况主要面向硬件卸载功能。 例如，低电源音频 (LPA) 在播放期间支持系统中，音频缓冲区大小或周期设置为 1 秒，以便在 CPU 不会唤醒经常处理小缓冲区 （例如，在每隔 10 毫秒）。

实现以及硬件卸载音频处理硬件卸载未提供最大程度提高能源效率的功能。

下图显示了音频处理对象体系结构。 关系图的右侧显示了向硬件进行通信的应用程序卸载 OSFX 和 OMFX 效果。

![显示应用程序调用 sfx mfx 和 efx 效果，然后调用到驱动程序和音频硬件的音频驱动程序体系结构](images/audio-hardware-offloaded-apo-overview.png)

## <a name="span-idimplementinghardwareoffloadedapoeffectsspanspan-idimplementinghardwareoffloadedapoeffectsspanspan-idimplementinghardwareoffloadedapoeffectsspanimplementing-hardware-offloaded-apo-effects"></a><span id="Implementing_Hardware_Offloaded_APO_Effects"></span><span id="implementing_hardware_offloaded_apo_effects"></span><span id="IMPLEMENTING_HARDWARE_OFFLOADED_APO_EFFECTS"></span>实现硬件卸载 APO 效果


硬件卸载 APO 必须遵循相同的基本要求和设计原则中所述[音频处理对象体系结构](audio-processing-object-architecture.md)并[实现音频处理对象](implementing-audio-processing-objects.md)。

**支持音频格式实现准则**

有关硬件卸载 a p o s，某些其他还必须考虑到支持的音频格式。

实现每个 APO [ **IAudioProcessingObject::IsInputFormatSupported** ](https://msdn.microsoft.com/library/windows/hardware/ff536511)音频图形生成过程中用来确定输出音频格式和是否任何格式转换的方法是所需。

```cpp
HRESULT IsInputFormatSupported(
  [in, optional]  IAudioMediaType *pOppositeFormat,
  [in, optional]  IAudioMediaType *pRequestedInputFormat,
  [out, optional] IAudioMediaType **ppSupportedInputFormat
);
```

卸载呈现终结点可以支持各种格式，包括支持的主机/系统 pin 呈现的默认格式。 卸载 APO 应支持所有这些格式，因此 （具有支持的格式） 呈现流无需通过任何其他格式转换。

卸载 SFX 可以实现格式的转换，并接受更广泛的格式。 例如，如果卸载 SFX 提供耳机虚拟化 （即，转换 5.1 通道音频为立体声），则它应返回 S\_为相应的输入/输出对此方法中的确定。

卸载 SFX 应查看卸载支持固定格式，并支持/扩展功能在一起。

卸载 MFX 不能更改输入流的格式，但它仍需要支持不同的格式提供的卸载终结点并消除任何不必要的格式转换。

在卸载 pin 中呈现，只有一个流上处于活动状态的 pin 并因此没有任何混合的流。 因此，处理的音频流级别和模式级别都不是必需的。 因此音频效果可能不需要启用作为流效果和模式的效果。 卸载终结点将支持更多的流，并根据系统的处理体系结构，卸载处理可能需要考虑到 SFX/MFX。 

**INF 文件条目**

实现以下的 INF 文件条目，可以定义将在卸载播放期间加载的效果。 INF 文件属性键指示音频终结点生成器 Clsid 为卸载未设置效果属性存储到。 此信息用于生成在音频图形的将用来通知哪些因素影响均已到位的上部级别应用。

|                                                                                                                                  |                                           |
|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------|
| **属性键**                                                                                                                 | **GUID**                                  |
| [PKEY\_FX\_Offload\_StreamEffectClsid](https://msdn.microsoft.com/library/windows/hardware/mt604869)                                                  | {D04E05A6-594B-4FB6-A80D-01AF5EED7D1D},11 |
| [PKEY\_FX\_Offload\_ModeEffectClsid](https://msdn.microsoft.com/library/windows/hardware/mt604868)                                                      | {D04E05A6-594B-4FB6-A80D-01AF5EED7D1D},12 |
| [PKEY\_SFX\_Offload\_ProcessingModes\_Supported\_For\_Streaming](https://msdn.microsoft.com/library/windows/hardware/mt604871) | {D3993A3F-99C2-4402-B5EC-A92A0367664B},11 |
| [PKEY\_MFX\_Offload\_ProcessingModes\_Supported\_For\_Streaming](https://msdn.microsoft.com/library/windows/hardware/mt604870) | {D3993A3F-99C2-4402-B5EC-A92A0367664B},12 |

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[实现音频处理对象](implementing-audio-processing-objects.md)  
[Windows 音频处理对象](windows-audio-processing-objects.md)  



