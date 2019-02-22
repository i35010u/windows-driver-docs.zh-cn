---
title: 结构字段的图片
description: 结构字段的图片
ms.assetid: fa058a30-74a2-4e8b-aa65-98ac5aa43e57
keywords:
- MPEG 2 WDK DirectX VA
- 字段运动补偿 WDK DirectX VA
- 字段 (16 x 8) 运动补偿 WDK DirectX VA
- 双素数运动补偿 WDK DirectX VA
- 16 x 8 运动补偿 WDK DirectX VA
- 预测阻止 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5c29a347277b369e1bcb0e60df0e216be6c72e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540438"
---
# <a name="field-structured-pictures"></a>结构字段的图片


## <span id="ddk_field_structured_pictures_gg"></span><span id="DDK_FIELD_STRUCTURED_PICTURES_GG"></span>


**字段 (16 x 16) MC**:字段 (16 x 16) 运动补偿类似于帧运动补偿，每个预测都具有 16 x 16 的形状。 但是，引用块数据顺序顶部字段或底部字段仅限线条 （不是混合交替顶级字段，底部字段线，如下所示渐进式运动） 构成。 为结构字段的图片中的所有动作补偿重新构造宏块是当前的帧缓冲区中作为都存储仅顺序顶字段或底部字段行。 顶部或底部字段目标由 mpeg-2*图片\_结构*变量。

**16 x 8 MC**:尽管这种类型的运动补偿的基本的预测块形状 （16 x 8 MC 和双素数 MC 字段） 的其他 16 x 8 形状相同，但它不会以相同方式进行分区宏块。 两个分区对应的宏块预测平面，而不是宏块中的顶部和底部字段的上限和下限的结果。 有关详细信息，请参阅中的"两个 mpeg-2 宏块 16 x 8 分区"图示[宏块分区](macroblock-partitioning.md)。 请注意，定位点的低 16 x 8 一半是 16 x 8 下半部分，不整个宏块，在窗口左上角的左上角与所有其他类型的运动补偿情况一样。

**双素数 MC**:在最低层上，是几乎双素数和使用双向预测结构字段的字段运动补偿之间没有区别。 中的帧缓冲区来选择从中形成引用块中显示的差异。 双素数运动结构字段的图片中的补偿始终包括两个 16 x 16 预测基块 （相同和奇偶校验预测相反）。

 

 





