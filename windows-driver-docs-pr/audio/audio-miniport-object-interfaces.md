---
title: 音频微型端口对象接口
description: 音频微型端口对象接口
ms.assetid: 2e79ad90-fecc-47a7-b487-809325a16239
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f9ddbbfe9e7b36676bf706c5d304d589c0668db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331453"
---
# <a name="audio-miniport-object-interfaces"></a>音频微型端口对象接口


## <span id="ddk_audio_miniport_object_interfaces_ks"></span><span id="DDK_AUDIO_MINIPORT_OBJECT_INTERFACES_KS"></span>


本部分中描述的音频的微型端口对象接口。 例如：

-   **IMiniport**，这是从中派生所有其他音频微型端口对象接口的基类型

-   音频的微型端口对象提供用于 Dmu，MIDI、 拓扑、 WaveCyclic、 WavePci 和 WaveRT 微型端口驱动程序的接口 (请参阅[支持设备](https://msdn.microsoft.com/library/windows/hardware/ff538398))，它派生自**IMiniport**

音频的微型端口对象接口是微型端口驱动程序提供给端口驱动程序的主接口。 适配器驱动程序可以通过将该设备的端口和微型端口驱动程序绑定在一起形成音频设备的 KS 筛选器。 绑定通过调用音频端口对象来实现[ **IPort::Init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)方法并传递对音频的微型端口对象的引用作为调用参数。 中的代码示例[子创建](https://msdn.microsoft.com/library/windows/hardware/ff538390)说明了此过程。

本部分讨论以下音频微型端口对象接口：

[IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698)

[IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699)

[IMiniportMidi](https://msdn.microsoft.com/library/windows/hardware/ff536703)

[IMiniportTopology](https://msdn.microsoft.com/library/windows/hardware/ff536712)

[IMiniportWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536714)

[IMiniportWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536724)

[IMiniportWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536737)

 

 





