---
title: 音频端口对象接口
description: 音频端口对象接口
ms.assetid: 16026a03-4859-4fe8-a106-0d8a2b2a7f14
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: df7b91e6fafc30108846aab2a161572a61f89d45
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355684"
---
# <a name="audio-port-object-interfaces"></a>音频端口对象接口


## <span id="ddk_audio_port_object_interfaces_ks"></span><span id="DDK_AUDIO_PORT_OBJECT_INTERFACES_KS"></span>


本部分介绍音频端口对象接口。 例如：

-   **IPort**，这是从中派生所有其他音频端口对象接口的基类型

-   音频 port 对象提供用于 Dmu，MIDI、 拓扑、 WaveCyclic、 WavePci 和 WaveRT 端口驱动程序的接口 (请参阅[支持设备](https://docs.microsoft.com/windows-hardware/drivers/audio/supporting-a-device))，它派生自**IPort**

音频端口对象接口是端口驱动程序提供给微型端口驱动程序的主接口。 适配器驱动程序可以通过将该设备的端口和微型端口驱动程序绑定在一起形成音频设备的 KS 筛选器。 绑定通过调用音频端口对象来实现[ **IPort::Init** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iport-init)方法并传递对音频的微型端口对象的引用作为调用参数。 中的代码示例[子创建](https://docs.microsoft.com/windows-hardware/drivers/audio/subdevice-creation)说明了此过程。

本部分介绍以下音频端口对象接口：

[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iport)

[IPortClsPower](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportclspower)

[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iportdmus)

[IPortMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportmidi)

[IPortTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iporttopology)

[IPortWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavecyclic)

[IPortWavePci](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85))

[IPortWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavert)

[IPortWMIRegistration](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwmiregistration)

 

 





