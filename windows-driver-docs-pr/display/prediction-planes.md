---
title: 预测平面
description: 预测平面
ms.assetid: 967d52d1-c4e1-4a81-a1ad-40a09040c3a8
keywords:
- 解码视频 WDK DirectX va，因此宏块预测
- 视频解码 WDK DirectX va，因此宏块预测
- 预测平面 WDK DirectX VA
- 宏块 WDK DirectX va，因此预测
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 728888ef51078b37d0919e734de807dd11c5a6fe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383992"
---
# <a name="prediction-planes"></a>预测平面


## <span id="ddk_prediction_planes_gg"></span><span id="DDK_PREDICTION_PLANES_GG"></span>


下图说明了构成最终预测之前存在的概念宏块预测平面。

![说明字段宏块预测的平面示例关系图](images/m2planes.png)

MPEG 2 具有两个平面： 向前和向后 （双向预测），或同一奇偶校验和相反的奇偶校验 （双质数）。 前向引用平面包含块的形式从最接近的以前我或 P 图片。 向后引用平面由块的形式从最接近的未来我 P 图片。

在 mpeg-1 和 mpeg-2 的情况下，预测平面之间的两个预测飞机相应的块像素值求平均值和舍入到最接近的整数的每个通过合并。 更加高级的预测方案，如 H.263 的重叠块运动补偿 (OBMC) 预测，拥有三个平面。

 

 





