---
title: KSPROPSETID\_DirectSound3DBuffer
description: KSPROPSETID\_DirectSound3DBuffer
ms.assetid: 38ee775a-9b6c-4803-a024-fecc852d122d
keywords:
- KSPROPSETID_DirectSound3DBuffer
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dedd099be95499d3ea2946c8692724ac6430c9c9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332538"
---
# <a name="kspropsetiddirectsound3dbuffer"></a>KSPROPSETID\_DirectSound3DBuffer


## <span id="ddk_kspropsetid_directsound3dbuffer_ks"></span><span id="DDK_KSPROPSETID_DIRECTSOUND3DBUFFER_KS"></span>


`KSPROPSETID_DirectSound3DBuffer`属性集包含实现所需的所有特定于设备的属性**IDirectSound3DBuffer**接口 （请参阅 Microsoft Windows SDK 文档）。 使用此属性集，直接 DirectSound 和 WDM 音频驱动程序之间传递 3D 缓冲区属性所指定的 API。 设置此属性由[ **KSNODETYPE\_3D\_效果**](ksnodetype-3d-effects.md)节点，用于处理 3D 缓冲区和 3D 侦听器属性。

在此集中的属性项由 KSPROPERTY\_DIRECTSOUND3DBUFFER 枚举值。

`KSPROPSETID_DirectSound3DBuffer`属性集包含以下属性：

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_所有**](ksproperty-directsound3dbuffer-all.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES**](ksproperty-directsound3dbuffer-coneangles.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEORIENTATION**](ksproperty-directsound3dbuffer-coneorientation.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEOUTSIDEVOLUME**](ksproperty-directsound3dbuffer-coneoutsidevolume.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_MAXDISTANCE**](ksproperty-directsound3dbuffer-maxdistance.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_MINDISTANCE**](ksproperty-directsound3dbuffer-mindistance.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_模式**](ksproperty-directsound3dbuffer-mode.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_位置**](ksproperty-directsound3dbuffer-position.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_速度**](ksproperty-directsound3dbuffer-velocity.md)

 

 





