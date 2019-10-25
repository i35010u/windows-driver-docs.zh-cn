---
title: KSPROPSETID\_Hrtf3d
description: KSPROPSETID\_Hrtf3d
ms.assetid: 8045991b-0409-445a-bd35-d9b8644f770e
keywords:
- KSPROPSETID_Hrtf3d
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 210a1002b65c040c4fd4c53f04454867b6383acd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830473"
---
# <a name="kspropsetid_hrtf3d"></a>KSPROPSETID\_Hrtf3d


## <span id="ddk_kspropsetid_hrtf3d_ks"></span><span id="DDK_KSPROPSETID_HRTF3D_KS"></span>


`KSPROPSETID_Hrtf3d` 属性集用于配置 DirectSound 缓冲区的3D 头相对传输功能（HRTF）。 此集包含 DirectSound pin 实例上3D 节点（[**KSNODETYPE\_3d\_效果**](ksnodetype-3d-effects.md)）的可选属性。

并非所有3D 节点都支持 HRTF 处理。 客户端可以将 HRTF 属性的基本支持查询发送到3D 节点，以确定该节点是否能够执行 HRTF 处理。 支持 `KSPROPSETID_Hrtf3d` 属性集的3D 节点必须支持这三个集中的所有三个属性。

此属性集的定义假定 HRTF 算法是使用无限脉冲响应（IIR）筛选器实现的，这些筛选器表示音频源在单个位置的效果。

数字筛选器通常具有初始暂时性响应。 在将源从一个位置移到下一个位置时，筛选器系数会发生变化，并且 HRTF 算法会将输出从旧位置的筛选器交叉淡化到新位置的筛选器。 [**KSDS3D\_HRTF\_INIT\_MSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_init_msg)结构的**FilterTransientMuteLength**成员指定延迟交叉淡入的样本数，以避免呈现新的筛选器初始暂时性。 在此期间，输出仅来自旧筛选器。 **FilterOverlapBufferLength**成员（相同结构）指定要对其进行静音和交叉淡化筛选器输出的样本总数。

当源从右半平面向左移动时，筛选器将切换。 此开关可能会导致弹出声音。 [**KSDS3D\_HRTF\_PARAMS\_MSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_params_msg)结构的**SWAPCHANNELS**成员通知 HRTF 算法交换输出，以将源位置反向转换为其他半平面。 **CrossFadeOutput**成员（相同结构）指示算法在跨 azimuth 角度零转换后，将输出通道交叉淡化。 KSDS3D\_HRTF\_INIT\_MSG 的**OutputOverlapBufferLength**成员指定发生此转换时要随其进行交叉淡化的样本的数量。

由于进行了对称，当 azimuth 角为零时，只需将部分筛选系数下载到 HRTF 算法。 KSDS3D\_HRTF\_参数的**ZeroAzimuth**成员\_MSG 指示何时发生此条件。

有关通过 DirectSound API 配置 HTRF 处理的信息，请参阅 Microsoft Windows SDK 文档。

`KSPROPSETID_Hrtf3d` 属性集包含以下三个成员：

[**KSPROPERTY\_HRTF3D\_\_格式的筛选器**](ksproperty-hrtf3d-filter-format.md)

[**KSPROPERTY\_HRTF3D\_INITIALIZE**](ksproperty-hrtf3d-initialize.md)

[**KSPROPERTY\_HRTF3D\_参数**](ksproperty-hrtf3d-params.md)

 

 





