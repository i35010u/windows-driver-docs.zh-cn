---
title: 音频端口对象接口
description: 音频端口对象接口
ms.assetid: 16026a03-4859-4fe8-a106-0d8a2b2a7f14
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f192cbc701ebe231046815391eaec1c5c9c09c5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208293"
---
# <a name="audio-port-object-interfaces"></a>音频端口对象接口


## <span id="ddk_audio_port_object_interfaces_ks"></span><span id="DDK_AUDIO_PORT_OBJECT_INTERFACES_KS"></span>


本部分介绍音频端口对象接口。 其中包括：

-   **IPort**，它是从中派生所有其他音频端口对象接口的基类型

-   音频端口对象提供 Dmu、MIDI、拓扑、WaveCyclic、WavePci 和 WaveRT 端口驱动程序的接口 (参阅支持从**IPort**派生的[设备](./supporting-a-device.md)) 

音频端口对象接口是端口驱动程序提供给微型端口驱动程序的主要接口。 适配器驱动程序通过将端口和微型端口驱动程序绑定在一起，形成音频设备的 KS 筛选器。 绑定是通过调用音频端口对象的 [**IPort：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init) 方法并将对音频微型端口对象的引用作为调用参数传递来实现的。 [Subdevice 创建](./subdevice-creation.md)中的代码示例演示了此过程。

本部分介绍以下音频端口对象接口：

[IPort](/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)

[IPortClsPower](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclspower)

[IPortDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)

[IPortMidi](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportmidi)

[IPortTopology](/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)

[IPortWaveCyclic](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic)

[IPortWavePci](/previous-versions/windows/hardware/drivers/ff536905(v=vs.85))

[IPortWaveRT](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavert)

[IPortWMIRegistration](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwmiregistration)

 

