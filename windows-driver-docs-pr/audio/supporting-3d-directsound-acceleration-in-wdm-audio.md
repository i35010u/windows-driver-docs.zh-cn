---
title: WDM 音频中支持三维 DirectSound 加速
description: WDM 音频中支持三维 DirectSound 加速
ms.assetid: 7524c15a-e487-43b6-9101-7cdd0c5e6e0c
keywords:
- 硬件加速 WDK DirectSound 3D 混合
- 3D 混合 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b464925a387ce6fc4021d82123863349779f6fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525272"
---
# <a name="supporting-3d-directsound-acceleration-in-wdm-audio"></a>WDM 音频中支持三维 DirectSound 加速


## <span id="supporting_3d_directsound_acceleration_in_wdm_audio"></span><span id="SUPPORTING_3D_DIRECTSOUND_ACCELERATION_IN_WDM_AUDIO"></span>


DirectSound 公开硬件加速 3D 混合的 WDM 音频微型端口驱动程序，满足以下要求：

-   Pin 必须满足中列出的要求[WDM 音频中支持 2D DirectSound 加速](supporting-2d-directsound-acceleration-in-wdm-audio.md)。

-   Pin 应包括 3D 节点 ([**KSNODETYPE\_3D\_效果**](https://msdn.microsoft.com/library/windows/hardware/ff537148)) 在其节点链中。 (请参阅[DirectSound 节点排序要求](directsound-node-ordering-requirements.md)。)

-   Pin 必须支持[KSPROPSETID\_DirectSound3DBuffer](https://msdn.microsoft.com/library/windows/hardware/ff537447) 3D 节点上设置的属性。

-   Pin 必须支持[KSPROPSETID\_DirectSound3DListener](https://msdn.microsoft.com/library/windows/hardware/ff537449) 3D 节点上设置的属性。

 

 




