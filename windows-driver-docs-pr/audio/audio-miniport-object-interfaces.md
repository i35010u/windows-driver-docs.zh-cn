---
title: 音频微型端口对象接口
description: 音频微型端口对象接口
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47f288dc9c49decf5e0d20293c1deea40aa2a873
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789389"
---
# <a name="audio-miniport-object-interfaces"></a>音频微型端口对象接口


## <span id="ddk_audio_miniport_object_interfaces_ks"></span><span id="DDK_AUDIO_MINIPORT_OBJECT_INTERFACES_KS"></span>


本部分介绍音频微型端口对象接口。 这些功能包括以下这些：

-   **IMiniport**，它是从其派生所有其他音频微型端口对象接口的基类型

-   音频微型端口对象提供 Dmu、MIDI、拓扑、WaveCyclic、WavePci 和 WaveRT 微型端口驱动程序的接口 (参阅 [支持](./supporting-a-device.md)从 **IMiniport** 派生的设备) 

音频微型端口对象接口是小型端口驱动程序提供给端口驱动程序的主要接口。 适配器驱动程序通过将端口和微型端口驱动程序绑定在一起，形成音频设备的 KS 筛选器。 绑定是通过调用音频端口对象的 [**IPort：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init) 方法并将对音频微型端口对象的引用作为调用参数传递来实现的。 [Subdevice 创建](./subdevice-creation.md)中的代码示例演示了此过程。

本部分介绍以下音频微型端口对象接口：

[IMiniport](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)

[IMiniportDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)

[IMiniportMidi](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)

[IMiniportTopology](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology)

[IMiniportWaveCyclic](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic)

[IMiniportWavePci](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci)

[IMiniportWaveRT](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert)

 

