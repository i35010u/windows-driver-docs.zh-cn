---
title: 支持在 WDM 音频中进行 3D DirectSound 加速
description: 支持在 WDM 音频中进行 3D DirectSound 加速
ms.assetid: 7524c15a-e487-43b6-9101-7cdd0c5e6e0c
keywords:
- 硬件加速 WDK DirectSound，3D 混合
- 3D 混合 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9e0058bc87fb61dd7f17315264ca8757527d3a1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206679"
---
# <a name="supporting-3d-directsound-acceleration-in-wdm-audio"></a>支持在 WDM 音频中进行 3D DirectSound 加速


## <span id="supporting_3d_directsound_acceleration_in_wdm_audio"></span><span id="SUPPORTING_3D_DIRECTSOUND_ACCELERATION_IN_WDM_AUDIO"></span>


DirectSound 公开适用于 WDM 音频微型端口驱动程序的硬件加速3D 混合，满足以下要求：

-   Pin 必须满足在 [WDM 音频中支持 2D DirectSound 加速中](supporting-2d-directsound-acceleration-in-wdm-audio.md)列出的要求。

-   Pin 应包括3D 节点 ([**KSNODETYPE \_ 3d \_ 效果**](./ksnodetype-3d-effects.md)) 在其节点链中。  (参阅 [DirectSound 节点顺序要求](directsound-node-ordering-requirements.md)。 ) 

-   Pin 必须支持3D 节点上设置的 [KSPROPSETID \_ DirectSound3DBuffer](./kspropsetid-directsound3dbuffer.md) 属性。

-   Pin 必须支持3D 节点上设置的 [KSPROPSETID \_ DirectSound3DListener](./kspropsetid-directsound3dlistener.md) 属性。

 

