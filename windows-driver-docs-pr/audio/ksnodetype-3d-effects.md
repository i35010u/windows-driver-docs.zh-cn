---
title: KSNODETYPE\_3D\_EFFECTS
description: KSNODETYPE\_3D\_EFFECTS
ms.assetid: 8b19423b-c1ad-4b59-bdae-a53bb99469ea
keywords:
- KSNODETYPE_3D_EFFECTS Audio Devices
topic_type:
- apiref
api_name:
- KSNODETYPE_3D_EFFECTS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2801d68257f98a42fdaef43ac5439deb8166f0a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359028"
---
# <a name="ksnodetype3deffects"></a>KSNODETYPE\_3D\_EFFECTS


## <span id="ddk_ksnodetype_3d_effects_ks"></span><span id="DDK_KSNODETYPE_3D_EFFECTS_KS"></span>


KSNODETYPE\_三维\_效果节点表示有关特定于设备的 3D HAL （硬件加速层） 的基础的 3D 效果处理器**IDirectSound3DBuffer**和**IDirectSound3DListener** Api （Microsoft Windows SDK 文档中所述）。 3D 节点都有一个与一个或两个通道的输入的流和一个输出流*n*通道。 它将在输出流的 3D 声音字段中定位的输入流的各个通道。

输入的流到三维节点通常包含一条通道。 DirectSound 8.0 及更高版本，则可以使用三维效果创建 mono PCM 缓冲区。 早期版本的 DirectSound，但是，支持具有 mono 和立体声输入流，3D 节点和驱动程序应支持这两个以确保与较旧的应用程序兼容性。

KSNODETYPE\_3D\_效果节点用来控制 DirectSound 扬声器配置，通过以下可选属性：

[**KSPROPERTY\_音频\_通道\_配置**](ksproperty-audio-channel-config.md)

[**KSPROPERTY\_音频\_立体声\_演讲者\_GEOMETRY**](ksproperty-audio-stereo-speaker-geometry.md)

有关详细信息，请参阅[DirectSound 扬声器配置设置](https://docs.microsoft.com/windows-hardware/drivers/audio/directsound-speaker-configuration-settings)。

此外，DirectSound 要求 KSNODETYPE\_3D\_效果节点支持以下 3D 侦听器和 3D 缓冲区属性：

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_所有**](ksproperty-directsound3dbuffer-all.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_位置**](ksproperty-directsound3dbuffer-position.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_速度**](ksproperty-directsound3dbuffer-velocity.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES**](ksproperty-directsound3dbuffer-coneangles.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEORIENTATION**](ksproperty-directsound3dbuffer-coneorientation.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEOUTSIDEVOLUME**](ksproperty-directsound3dbuffer-coneoutsidevolume.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_MINDISTANCE**](ksproperty-directsound3dbuffer-mindistance.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_MAXDISTANCE**](ksproperty-directsound3dbuffer-maxdistance.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_模式**](ksproperty-directsound3dbuffer-mode.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_所有**](ksproperty-directsound3dlistener-all.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_位置**](ksproperty-directsound3dlistener-position.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_速度**](ksproperty-directsound3dlistener-velocity.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_方向**](ksproperty-directsound3dlistener-orientation.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR**](ksproperty-directsound3dlistener-rollofffactor.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_DOPPLERFACTOR**](ksproperty-directsound3dlistener-dopplerfactor.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_批处理**](ksproperty-directsound3dlistener-batch.md)

KSNODETYPE\_3D\_效果节点可能会实现头相对传递函数 (HRTF)，这种情况下，它应该支持以下可选属性：

[**KSPROPERTY\_HRTF3D\_FILTER\_FORMAT**](ksproperty-hrtf3d-filter-format.md)

[**KSPROPERTY\_HRTF3D\_初始化**](ksproperty-hrtf3d-initialize.md)

[**KSPROPERTY\_HRTF3D\_PARAMS**](ksproperty-hrtf3d-params.md)

KSNODETYPE\_3D\_效果节点可能会实现 interaural 时间延迟 (ITD) 算法，这种情况下，它应该支持以下可选属性：

[**KSPROPERTY\_ITD3D\_PARAMS**](ksproperty-itd3d-params.md)

 

 





