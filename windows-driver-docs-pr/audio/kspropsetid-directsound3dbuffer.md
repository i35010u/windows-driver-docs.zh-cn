---
title: KSPROPSETID \_ DirectSound3DBuffer
description: KSPROPSETID \_ DirectSound3DBuffer
keywords:
- KSPROPSETID_DirectSound3DBuffer
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cfb5c87a932573046b59a06a15a4dc68a165f0d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801107"
---
# <a name="kspropsetid_directsound3dbuffer"></a>KSPROPSETID \_ DirectSound3DBuffer


## <span id="ddk_kspropsetid_directsound3dbuffer_ks"></span><span id="DDK_KSPROPSETID_DIRECTSOUND3DBUFFER_KS"></span>


`KSPROPSETID_DirectSound3DBuffer`属性集包含实现 **IDirectSound3DBuffer** 接口所需的所有特定于设备的属性 (参阅 Microsoft Windows SDK 文档) 。 使用此属性集，由 API 指定的3D 缓冲区属性直接在 DirectSound 与 WDM 音频驱动程序之间传递。 此属性集由 KSNODETYPE 的 " [**\_ 三维 \_ 效果**](ksnodetype-3d-effects.md) " 节点进行处理，该节点处理3d 缓冲区和3d 侦听器的属性。

此集中的属性项由 KSPROPERTY \_ DIRECTSOUND3DBUFFER 枚举值指定。

`KSPROPSETID_DirectSound3DBuffer`属性集包含以下属性：

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ ALL**](ksproperty-directsound3dbuffer-all.md)

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ CONEANGLES**](ksproperty-directsound3dbuffer-coneangles.md)

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ CONEORIENTATION**](ksproperty-directsound3dbuffer-coneorientation.md)

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ CONEOUTSIDEVOLUME**](ksproperty-directsound3dbuffer-coneoutsidevolume.md)

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ MAXDISTANCE**](ksproperty-directsound3dbuffer-maxdistance.md)

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ MINDISTANCE**](ksproperty-directsound3dbuffer-mindistance.md)

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ 模式**](ksproperty-directsound3dbuffer-mode.md)

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ 位置**](ksproperty-directsound3dbuffer-position.md)

[**KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ 速度**](ksproperty-directsound3dbuffer-velocity.md)

 

 





