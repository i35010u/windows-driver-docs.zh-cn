---
title: 音频微型端口对象接口
description: 音频微型端口对象接口
ms.assetid: 2e79ad90-fecc-47a7-b487-809325a16239
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 704d8bf992c7357dd2e948251265fac1090a79a7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833676"
---
# <a name="audio-miniport-object-interfaces"></a>音频微型端口对象接口


## <span id="ddk_audio_miniport_object_interfaces_ks"></span><span id="DDK_AUDIO_MINIPORT_OBJECT_INTERFACES_KS"></span>


本部分介绍音频微型端口对象接口。 这包括：

-   **IMiniport**，它是从其派生所有其他音频微型端口对象接口的基类型

-   音频微型端口对象为 Dmu、MIDI、拓扑、WaveCyclic、WavePci 和 WaveRT 微型端口驱动程序（请参阅[支持设备](https://docs.microsoft.com/windows-hardware/drivers/audio/supporting-a-device)）提供了一个接口，该接口派生自**IMiniport**

音频微型端口对象接口是小型端口驱动程序提供给端口驱动程序的主要接口。 适配器驱动程序通过将端口和微型端口驱动程序绑定在一起，形成音频设备的 KS 筛选器。 绑定是通过调用音频端口对象的[**IPort：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)方法并将对音频微型端口对象的引用作为调用参数传递来实现的。 [Subdevice 创建](https://docs.microsoft.com/windows-hardware/drivers/audio/subdevice-creation)中的代码示例演示了此过程。

本部分介绍以下音频微型端口对象接口：

[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)

[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)

[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)

[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology)

[IMiniportWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic)

[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci)

[IMiniportWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert)

 

 





