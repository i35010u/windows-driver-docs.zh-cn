---
title: 预测平面
description: 预测平面
keywords:
- 解码视频 WDK DirectX VA，宏块预测
- 视频解码 WDK DirectX VA，宏块预测
- 预测平面 WDK DirectX VA
- macroblocks WDK DirectX VA，预测
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41f0cd7d117f271d713f0168883645b796786576
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833071"
---
# <a name="prediction-planes"></a>预测平面


## <span id="ddk_prediction_planes_gg"></span><span id="DDK_PREDICTION_PLANES_GG"></span>


下图说明了在形成最终预测之前存在的概念宏块预测平面。

![说明字段宏块预测的平面示例的关系图](images/m2planes.png)

MPEG-2 有两个平面：向前和向后 (双向预测) ，或相同的奇偶校验， (双质数) 。 正向引用平面由最近的前面的 I 或 P 图片中的块组成。 向后引用平面由最近的未来 I 或 P 图片中的块组成。

在 MPEG-2 和 MPEG-2 情况下，预测平面将按两个预测平面的相应块像素值的平均值进行合并，并将每个值向上舍入到最接近的整数。 更复杂的预测方案，如263's 重叠的块运动 (OBMC) 预测，具有三个平面。

 

 





