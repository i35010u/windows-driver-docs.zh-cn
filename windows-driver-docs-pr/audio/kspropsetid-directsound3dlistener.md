---
title: KSPROPSETID \_ DirectSound3DListener
description: KSPROPSETID \_ DirectSound3DListener
keywords:
- KSPROPSETID_DirectSound3DListener
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3259d413c367e39869d2030546baa6906da5cde7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801105"
---
# <a name="kspropsetid_directsound3dlistener"></a>KSPROPSETID \_ DirectSound3DListener


## <span id="ddk_kspropsetid_directsound3dlistener_ks"></span><span id="DDK_KSPROPSETID_DIRECTSOUND3DLISTENER_KS"></span>


`KSPROPSETID_DirectSound3DListener`属性集包含实现 **IDirectSound3DListener** 接口所需的所有特定于设备的属性 (参阅 Microsoft Windows SDK 文档) 。 使用此属性集，由 API 指定的3D 缓冲区属性直接在 DirectSound 与 WDM 音频驱动程序之间传递。 此属性集由 [**KSNODETYPE \_ 3d \_ 效果**](ksnodetype-3d-effects.md) 节点处理。 此节点同时处理3D 缓冲区和3D 侦听器属性，因此 WDM 音频驱动程序应将任何更新的侦听器属性应用于共享同一侦听器的其他缓冲区。

此集中的属性项由 KSPROPERTY \_ DIRECTSOUND3DLISTENER 枚举值指定。

`KSPROPSETID_DirectSound3DListener`属性集包含以下属性：

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ ALL**](ksproperty-directsound3dlistener-all.md)

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 分配**](ksproperty-directsound3dlistener-allocation.md)

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 批处理**](ksproperty-directsound3dlistener-batch.md)

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DOPPLERFACTOR**](ksproperty-directsound3dlistener-dopplerfactor.md)

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 方向**](ksproperty-directsound3dlistener-orientation.md)

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 位置**](ksproperty-directsound3dlistener-position.md)

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ ROLLOFFFACTOR**](ksproperty-directsound3dlistener-rollofffactor.md)

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 速度**](ksproperty-directsound3dlistener-velocity.md)

 

 





