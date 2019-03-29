---
title: KSPROPSETID\_DirectSound3DListener
description: KSPROPSETID\_DirectSound3DListener
ms.assetid: 37eef2cb-5b45-4ff8-abb9-a685f0b290e3
keywords:
- KSPROPSETID_DirectSound3DListener
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdea3c9034a9acd8c404e9c8fe2e17fcdca578ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567914"
---
# <a name="kspropsetiddirectsound3dlistener"></a>KSPROPSETID\_DirectSound3DListener


## <span id="ddk_kspropsetid_directsound3dlistener_ks"></span><span id="DDK_KSPROPSETID_DIRECTSOUND3DLISTENER_KS"></span>


`KSPROPSETID_DirectSound3DListener`属性集包含实现所需的所有特定于设备的属性**IDirectSound3DListener**接口 （请参阅 Microsoft Windows SDK 文档）。 使用此属性集，直接 DirectSound 和 WDM 音频驱动程序之间传递 3D 缓冲区属性所指定的 API。 设置此属性由[ **KSNODETYPE\_3D\_效果**](ksnodetype-3d-effects.md)节点。 此节点处理这两个 3D 缓冲区和 3D 侦听器属性，因此 WDM 音频驱动程序应将任何更新的侦听器属性应用于其他共享相同的侦听器的缓冲区。

在此集中的属性项由 KSPROPERTY\_DIRECTSOUND3DLISTENER 枚举值。

`KSPROPSETID_DirectSound3DListener`属性集包含以下属性：

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_所有**](ksproperty-directsound3dlistener-all.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_分配**](ksproperty-directsound3dlistener-allocation.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_批处理**](ksproperty-directsound3dlistener-batch.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_DOPPLERFACTOR**](ksproperty-directsound3dlistener-dopplerfactor.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_方向**](ksproperty-directsound3dlistener-orientation.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_位置**](ksproperty-directsound3dlistener-position.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR**](ksproperty-directsound3dlistener-rollofffactor.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_速度**](ksproperty-directsound3dlistener-velocity.md)

 

 





