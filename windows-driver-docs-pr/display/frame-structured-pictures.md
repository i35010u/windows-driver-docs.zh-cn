---
title: 结构帧的图片
description: 结构帧的图片
ms.assetid: 6449492e-06b5-4b8b-9e0d-a2e80272f062
keywords:
- MPEG 2 WDK DirectX VA
- 帧运动补偿 WDK DirectX VA
- 字段 (16 x 8) 运动补偿 WDK DirectX VA
- 双素数运动补偿 WDK DirectX VA
- 16 x 8 运动补偿 WDK DirectX VA
- 预测阻止 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91dd5bb48a00888860c404428a92ac1599e10b2e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521384"
---
# <a name="frame-structured-pictures"></a>结构帧的图片


## <span id="ddk_frame_structured_pictures_gg"></span><span id="DDK_FRAME_STRUCTURED_PICTURES_GG"></span>


**帧 MC**:帧运动补偿有 16 x 16 预测块形状，类似于 mpeg-1 预测。 这是仅渐进式样式运动补偿内 mpeg-2 (所指定的*运动\_类型*MPEG 2 中用户定义变量)。 没有任何一个*预测平面*（只进或仅向后） 或两个 （双向） 由*宏块\_类型*mpeg-2 变量。 从帧缓冲区中的连续帧行形成引用块。 帧缓冲区被选中的解码过程的语义。 后半部分示例内插 (mpeg-2 部分 7.6.4) 和双向内插 (mpeg-2 部分 7.6.7.1) 具有相同的求平均值操作，如 mpeg-1 用例中所示。

**字段 (16 x 8) MC**:字段 (16 x 8) 运动补偿已包含 top 16 x 8 预测块和底部 16 x 8 预测块的每个预测平面 （向前和向后方向）。 可能从上面的字段或参考帧的底部字段中由 mpeg-2 变量提取引用块对应于每个预测块*运动\_垂直\_字段\_选择* \[ *r*\]\[*s*\]。 有两种可能的字段 (16 x 8) 运动补偿：

-   两个预测块，用于一次预测平面 （向前或向后仅使用两个预测块，每个宏块的预测） 的一组。

-   两个设置的两个预测块为两个预测平面 （双向预测与宏块中的四个预测块）。

**双素数 MC**:字段 (16 x 8) 运动补偿的更多信息，如双素数运动补偿已包含 top 的每个平面 （奇偶校验） 和下 16 x 8 形状。 同一和奇偶校验平面相反组合在一起求平均值操作中。 此求平均值操作等同于用于 MPEG 2 中的其他动作类型的双向内插。 其他运动补偿与类型不同，双重素数宏块始终包含两个集的预测块 （的相同和相反的奇偶校验） 总计的每个宏块的四个预测块。

 

 





