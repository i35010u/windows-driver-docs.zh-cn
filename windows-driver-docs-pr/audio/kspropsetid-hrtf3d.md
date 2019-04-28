---
title: KSPROPSETID\_Hrtf3d
description: KSPROPSETID\_Hrtf3d
ms.assetid: 8045991b-0409-445a-bd35-d9b8644f770e
keywords:
- KSPROPSETID_Hrtf3d
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffd94c3b3916952d762fc25583159057164b4008
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332513"
---
# <a name="kspropsetidhrtf3d"></a>KSPROPSETID\_Hrtf3d


## <span id="ddk_kspropsetid_hrtf3d_ks"></span><span id="DDK_KSPROPSETID_HRTF3D_KS"></span>


`KSPROPSETID_Hrtf3d`属性集用于配置 DirectSound 缓冲区的 3D 头相对传输函数 (HRTF)。 本集包含三维节点的可选属性 ([**KSNODETYPE\_3D\_效果**](ksnodetype-3d-effects.md)) DirectSound pin 实例上。

不是所有 3D 节点支持 HRTF 处理。 客户端可以发送到三维的节点，以确定该节点是否能够执行 HRTF 处理 HRTF 属性的基本支持查询。 支持的 3D 节点`KSPROPSETID_Hrtf3d`属性集必须支持所有这三个属性集中。

此属性集的定义假定 HRTF 算法实现与无限脉冲响应 (IIR) 过滤器，表示音频源中的单个位置的效果。

数字筛选器通常具有暂时性的初始响应。 当将源从一个位置移动到下一步，过滤器系数将更改和 HRTF 算法跨淡化到新位置处的筛选器中的旧位置筛选器的输出。 **FilterTransientMuteLength**的成员[ **KSDS3D\_HRTF\_INIT\_MSG** ](https://msdn.microsoft.com/library/windows/hardware/ff537106)结构指定的数目为了避免呈现新筛选器的初始暂时性淡延迟跨所依据的示例。 在此期间，输出来自旧筛选器。 **FilterOverlapBufferLength**成员 （相同的结构） 指定要对其设为静音的样本总数并交叉淡入淡出该筛选器输出。

当源向左移动右半面中时，切换筛选器。 此开关可能会导致声音 pop。 **SwapChannels**的成员[ **KSDS3D\_HRTF\_PARAMS\_MSG** ](https://msdn.microsoft.com/library/windows/hardware/ff537108)结构指示要交换的 HRTF 算法输出到其他半面反转的源位置。 **CrossFadeOutput**成员 （相同的结构） 会告知要跨的淡入淡出的输出通道后跨方位转换角度零的算法。 **OutputOverlapBufferLength** KSDS3D 成员\_HRTF\_INIT\_消息指定要对其进行交叉淡入此转换发生时的样本数。

由于对称性，一半的过滤器系数需要下载到 HRTF 算法时的方位角度为零。 **ZeroAzimuth** KSDS3D 成员\_HRTF\_PARAMS\_消息指示当发生这种情况。

有关配置 HTRF 处理通过 DirectSound API 的信息，请参阅 Microsoft Windows SDK 文档。

`KSPROPSETID_Hrtf3d`属性集包含以下三个成员：

[**KSPROPERTY\_HRTF3D\_FILTER\_FORMAT**](ksproperty-hrtf3d-filter-format.md)

[**KSPROPERTY\_HRTF3D\_初始化**](ksproperty-hrtf3d-initialize.md)

[**KSPROPERTY\_HRTF3D\_PARAMS**](ksproperty-hrtf3d-params.md)

 

 





