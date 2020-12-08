---
title: 场结构化图片
description: 场结构化图片
keywords:
- MPEG-2 WDK DirectX VA
- 现场运动补偿-DirectX VA
- 现场 (16x8) 运动补偿 WDK DirectX VA
- 双重运动补偿 WDK DirectX VA
- 16x8 运动补偿 WDK DirectX VA
- 预测块 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98e7744b38518254fac6a16456c11ef36f81f50c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803575"
---
# <a name="field-structured-pictures"></a>场结构化图片


## <span id="ddk_field_structured_pictures_gg"></span><span id="DDK_FIELD_STRUCTURED_PICTURES_GG"></span>


**字段 (16x16) MC**：字段 (16x16) 运动补偿类似于帧运动补偿，因为每个预测都有一个16x16 形状。 不过，引用块数据是从顺序排名靠前的字段或底部的字段中生成的，它们仅 (与渐进式运动) 不混合的其他字段行和底部字段。 与字段结构化图片中的所有运动补偿一样，重建后的宏块仅存储在当前帧缓冲区中，只是按顺序排列的顶级字段行或底部字段行。 顶部或底部的字段目标由 MPEG-2 *图片 \_ 结构* 变量确定。

**16X8 MC**：尽管此类运动补偿的基本预测块形状与其他16x8 形状 (现场 16x8 MC 和双质数 MC) 相同，但它不会以相同的方式对宏块进行分区。 这两个分区对应于宏块预测平面的上半部分和下半部分，而不是对应于宏块中的顶部和底部字段。 有关详细信息，请参阅 [宏块分区](macroblock-partitioning.md)中的 "两个 mpeg-4 宏块16x8 分区" 插图。 请注意，较低的16x8 半的定位点是16x8 下半部分的左上角，而不是整个宏块的左上角，与所有其他类型的运动补偿的情况一样。

**双上标 MC**：在最低层上，与双向预测相比，双重质数与字段结构化字段运动补偿几乎没有区别。 不同之处在于引用块构成的帧缓冲区选择。 字段结构化图片中的双质数运动补偿始终包含两个16x16 预测块 (相同和相反的奇偶校验预测) 。

 

 





