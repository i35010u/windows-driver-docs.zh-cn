---
title: KSNODETYPE \_ 三维 \_ 效果
description: KSNODETYPE \_ 三维 \_ 效果
ms.assetid: 8b19423b-c1ad-4b59-bdae-a53bb99469ea
keywords:
- KSNODETYPE_3D_EFFECTS 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_3D_EFFECTS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2abebdcec3ce07edd414a4e843e3d6a9189f4337
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207040"
---
# <a name="ksnodetype_3d_effects"></a>KSNODETYPE \_ 三维 \_ 效果


## <span id="ddk_ksnodetype_3d_effects_ks"></span><span id="DDK_KSNODETYPE_3D_EFFECTS_KS"></span>


"KSNODETYPE \_ 三维 \_ 效果" 节点表示特定于设备的 3d (硬件加速层) 的3d 效果处理器，该处理器是 **IDirectSound3DBuffer** 和 **IDirectSound3DListener** api 的基础， (Microsoft Windows SDK 文档) 中所述。 3D 节点有一个输入流，其中包含一个或两个通道，一个输出流包含 *n* 个通道。 它将输入流的单个通道定位在输出流的三维声音字段内。

三维节点的输入流通常包含单个通道。 在 DirectSound 8.0 和更高版本中，仅可以通过三维效果创建 mono PCM 缓冲区。 但是，早期版本的 DirectSound 支持带有 mono 和立体声输入流的3D 节点，并且驱动程序应同时支持这两者，以确保与较旧的应用程序兼容。

KSNODETYPE \_ 3d \_ 效果节点用于通过以下可选属性控制 DirectSound 发言人配置：

[**KSPROPERTY \_ 音频 \_ 通道 \_ 配置**](ksproperty-audio-channel-config.md)

[**KSPROPERTY \_ 音频 \_ 立体声 \_ 扬声器 \_ 几何**](ksproperty-audio-stereo-speaker-geometry.md)

有关详细信息，请参阅 [DirectSound 演讲者-配置设置](./directsound-speaker-configuration-settings.md)。

此外，DirectSound 要求 KSNODETYPE \_ 三维 \_ 效果节点支持以下3d 侦听器和3d 缓冲区属性：

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ ALL**](ksproperty-directsound3dbuffer-all.md)

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ 位置**](ksproperty-directsound3dbuffer-position.md)

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ 速度**](ksproperty-directsound3dbuffer-velocity.md)

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ CONEANGLES**](ksproperty-directsound3dbuffer-coneangles.md)

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ CONEORIENTATION**](ksproperty-directsound3dbuffer-coneorientation.md)

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ CONEOUTSIDEVOLUME**](ksproperty-directsound3dbuffer-coneoutsidevolume.md)

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ MINDISTANCE**](ksproperty-directsound3dbuffer-mindistance.md)

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ MAXDISTANCE**](ksproperty-directsound3dbuffer-maxdistance.md)

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ 模式**](ksproperty-directsound3dbuffer-mode.md)

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ ALL**](ksproperty-directsound3dlistener-all.md)

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 位置**](ksproperty-directsound3dlistener-position.md)

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 速度**](ksproperty-directsound3dlistener-velocity.md)

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 方向**](ksproperty-directsound3dlistener-orientation.md)

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ ROLLOFFFACTOR**](ksproperty-directsound3dlistener-rollofffactor.md)

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DOPPLERFACTOR**](ksproperty-directsound3dlistener-dopplerfactor.md)

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 批处理**](ksproperty-directsound3dlistener-batch.md)

KSNODETYPE \_ 3d \_ 效果节点可能 (HRTF) 实现头相对传输功能，在这种情况下，它应支持以下可选属性：

[**KSPROPERTY \_ HRTF3D \_ 筛选器 \_ 格式**](ksproperty-hrtf3d-filter-format.md)

[**KSPROPERTY \_ HRTF3D \_ INITIALIZE**](ksproperty-hrtf3d-initialize.md)

[**KSPROPERTY \_ HRTF3D \_ 参数**](ksproperty-hrtf3d-params.md)

KSNODETYPE \_ 3d \_ 效果节点可以 (ITD) 算法实现 interaural 时间延迟，在这种情况下，它应支持以下可选属性：

[**KSPROPERTY \_ ITD3D \_ 参数**](ksproperty-itd3d-params.md)

 

