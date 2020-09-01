---
title: KSPROPSETID \_ Hrtf3d
description: KSPROPSETID \_ Hrtf3d
ms.assetid: 8045991b-0409-445a-bd35-d9b8644f770e
keywords:
- KSPROPSETID_Hrtf3d
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02201ccc8f3d49dba627a00c9b66633ee36afd00
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208847"
---
# <a name="kspropsetid_hrtf3d"></a>KSPROPSETID \_ Hrtf3d


## <span id="ddk_kspropsetid_hrtf3d_ks"></span><span id="DDK_KSPROPSETID_HRTF3D_KS"></span>


`KSPROPSETID_Hrtf3d`属性集用于配置 DirectSound 缓冲区 (HRTF) 的3d 头相对传输函数。 此集包含3D 节点的可选属性， (DirectSound pin 实例上的 [**KSNODETYPE \_ 3d \_ 效果**](ksnodetype-3d-effects.md)) 。

并非所有3D 节点都支持 HRTF 处理。 客户端可以将 HRTF 属性的基本支持查询发送到3D 节点，以确定该节点是否能够执行 HRTF 处理。 支持属性集的3D 节点 `KSPROPSETID_Hrtf3d` 必须支持集中所有三个属性。

此属性集的定义假定 HRTF 算法是使用无限脉冲响应实现的， () IIR 表示音频源在单个位置的影响的筛选器。

数字筛选器通常具有初始暂时性响应。 在将源从一个位置移到下一个位置时，筛选器系数会发生变化，并且 HRTF 算法会将输出从旧位置的筛选器交叉淡化到新位置的筛选器。 [**KSDS3D \_ HRTF \_ INIT \_ 消息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_init_msg)结构的**FilterTransientMuteLength**成员指定延迟交叉淡入的样本数，以避免呈现新筛选器的初始暂时性。 在此期间，输出仅来自旧筛选器。 **FilterOverlapBufferLength**成员 (相同的结构) 指定对筛选输出进行静音和交叉淡化的样本总数。

当源从右半平面向左移动时，筛选器将切换。 此开关可能会导致弹出声音。 [**KSDS3D \_ HRTF \_ PARAMS \_ 消息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_params_msg)结构的**SwapChannels**成员通知 HRTF 算法交换输出，以将源位置反向转换为其他半平面。 **CrossFadeOutput**成员 (相同的结构) 告知算法在 azimuth 角零间转换后，将输出通道交叉淡化。 KSDS3D **OutputOverlapBufferLength** \_ HRTF INIT MSG 的 OutputOverlapBufferLength \_ 成员 \_ 指定发生此转换时要随其进行交叉淡化的样本的数量。

由于进行了对称，当 azimuth 角为零时，只需将部分筛选系数下载到 HRTF 算法。 KSDS3D **ZeroAzimuth** \_ HRTF PARAMS MSG 的 ZeroAzimuth \_ 成员 \_ 指示何时发生此条件。

有关通过 DirectSound API 配置 HTRF 处理的信息，请参阅 Microsoft Windows SDK 文档。

`KSPROPSETID_Hrtf3d`属性集包含以下三个成员：

[**KSPROPERTY \_ HRTF3D \_ 筛选器 \_ 格式**](ksproperty-hrtf3d-filter-format.md)

[**KSPROPERTY \_ HRTF3D \_ INITIALIZE**](ksproperty-hrtf3d-initialize.md)

[**KSPROPERTY \_ HRTF3D \_ 参数**](ksproperty-hrtf3d-params.md)

 

