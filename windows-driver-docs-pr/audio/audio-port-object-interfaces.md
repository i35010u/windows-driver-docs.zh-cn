---
title: 音频端口对象接口
description: 音频端口对象接口
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aca56ae55644e7fdaba60ea119222b413fdfc371
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789383"
---
# <a name="audio-port-object-interfaces"></a>音频端口对象接口

## <span id="ddk_audio_port_object_interfaces_ks"></span><span id="DDK_AUDIO_PORT_OBJECT_INTERFACES_KS"></span>


本部分介绍音频端口对象接口。 这些功能包括以下这些：

- **IPort**，它是从中派生所有其他音频端口对象接口的基类型

- 音频端口对象提供 Dmu、MIDI、拓扑、WaveCyclic、WavePci 和 WaveRT 端口驱动程序的接口 (参阅支持从 **IPort** 派生的 [设备](./supporting-a-device.md)) 

音频端口对象接口是端口驱动程序提供给微型端口驱动程序的主要接口。 适配器驱动程序通过将端口和微型端口驱动程序绑定在一起，形成音频设备的 KS 筛选器。 绑定是通过调用音频端口对象的 [**IPort：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init) 方法并将对音频微型端口对象的引用作为调用参数传递来实现的。 [Subdevice 创建](./subdevice-creation.md)中的代码示例演示了此过程。

本部分介绍以下音频端口对象接口：

[IPort](/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)

[IPortClsPower](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclspower)

[IPortDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)

[IPortMidi](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportmidi)

[IPortTopology](/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)

[IPortWaveCyclic](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic)

[IPortWavePci](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavepci)

[IPortWaveRT](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavert)

[IPortWMIRegistration](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwmiregistration)
