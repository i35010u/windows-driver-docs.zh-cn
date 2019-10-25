---
title: 音频端口对象接口
description: 音频端口对象接口
ms.assetid: 16026a03-4859-4fe8-a106-0d8a2b2a7f14
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57715d44ef3065b0378b4073210eb33f0133dcd0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831348"
---
# <a name="audio-port-object-interfaces"></a>音频端口对象接口


## <span id="ddk_audio_port_object_interfaces_ks"></span><span id="DDK_AUDIO_PORT_OBJECT_INTERFACES_KS"></span>


本部分介绍音频端口对象接口。 这包括：

-   **IPort**，它是从中派生所有其他音频端口对象接口的基类型

-   音频端口对象为 Dmu、MIDI、拓扑、WaveCyclic、WavePci 和 WaveRT 端口驱动程序（请参阅[支持设备](https://docs.microsoft.com/windows-hardware/drivers/audio/supporting-a-device)）提供了一个接口，该接口派生自**IPort**

音频端口对象接口是端口驱动程序提供给微型端口驱动程序的主要接口。 适配器驱动程序通过将端口和微型端口驱动程序绑定在一起，形成音频设备的 KS 筛选器。 绑定是通过调用音频端口对象的[**IPort：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)方法并将对音频微型端口对象的引用作为调用参数传递来实现的。 [Subdevice 创建](https://docs.microsoft.com/windows-hardware/drivers/audio/subdevice-creation)中的代码示例演示了此过程。

本部分介绍以下音频端口对象接口：

[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)

[IPortClsPower](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclspower)

[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)

[IPortMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportmidi)

[IPortTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)

[IPortWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic)

[IPortWavePci](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85))

[IPortWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavert)

[IPortWMIRegistration](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwmiregistration)

 

 





