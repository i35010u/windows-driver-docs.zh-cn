---
title: 音频端口对象接口
description: 音频端口对象接口
ms.assetid: 16026a03-4859-4fe8-a106-0d8a2b2a7f14
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40abbf4a9f00d2492da8106a2b40d0c5b9ee17f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331425"
---
# <a name="audio-port-object-interfaces"></a>音频端口对象接口


## <span id="ddk_audio_port_object_interfaces_ks"></span><span id="DDK_AUDIO_PORT_OBJECT_INTERFACES_KS"></span>


本部分介绍音频端口对象接口。 例如：

-   **IPort**，这是从中派生所有其他音频端口对象接口的基类型

-   音频 port 对象提供用于 Dmu，MIDI、 拓扑、 WaveCyclic、 WavePci 和 WaveRT 端口驱动程序的接口 (请参阅[支持设备](https://msdn.microsoft.com/library/windows/hardware/ff538398))，它派生自**IPort**

音频端口对象接口是端口驱动程序提供给微型端口驱动程序的主接口。 适配器驱动程序可以通过将该设备的端口和微型端口驱动程序绑定在一起形成音频设备的 KS 筛选器。 绑定通过调用音频端口对象来实现[ **IPort::Init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)方法并传递对音频的微型端口对象的引用作为调用参数。 中的代码示例[子创建](https://msdn.microsoft.com/library/windows/hardware/ff538390)说明了此过程。

本部分介绍以下音频端口对象接口：

[IPort](https://msdn.microsoft.com/library/windows/hardware/ff536842)

[IPortClsPower](https://msdn.microsoft.com/library/windows/hardware/ff536844)

[IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)

[IPortMidi](https://msdn.microsoft.com/library/windows/hardware/ff536891)

[IPortTopology](https://msdn.microsoft.com/library/windows/hardware/ff536896)

[IPortWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536899)

[IPortWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536905)

[IPortWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536920)

[IPortWMIRegistration](https://msdn.microsoft.com/library/windows/hardware/ff536935)

 

 





