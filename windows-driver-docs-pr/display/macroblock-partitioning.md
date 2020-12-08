---
title: 宏块分区
description: 宏块分区
keywords:
- 解码视频 WDK DirectX VA，宏块预测
- 视频解码 WDK DirectX VA，宏块预测
- macroblocks WDK DirectX VA，预测
- 色度预测块 WDK DirectX VA
- 预测块 WDK DirectX VA
- macroblocks WDK DirectX VA，分区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5493711d7c72b5b8e7df2533bc5d77a6a6f839a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793931"
---
# <a name="macroblock-partitioning"></a>宏块分区


## <span id="ddk_macroblock_partitioning_gg"></span><span id="DDK_MACROBLOCK_PARTITIONING_GG"></span>


Macroblocks 可以分解为以下段。  (这是为了划分具有不同特征的区域。 ) 下图显示了如何将 macroblocks 分解为以下段。

![阐释基本宏块分区方案的关系图](images/portschem.png)

在 MPEG-2 情况下，框架图片中字段结构化宏块的上和下部分表示在不同的时间段内捕获的两个不同字段中的行，最多 fiftieth 一次。 因此，如果在宏块所涵盖的帧区域的两个字段之间发生了重大变动，则顶部和底部部分可能包含完全非相关的内容。 如下图中所示，附加的16x8 方案添加在字段结构化图片中，以提供更精细的预测粒度，更好地适应边缘和具有不同动作特征的小对象。

![说明两个 mpeg-2 宏块16x8 分区的示意图](images/m2macro.png)

预测块本身是一个形状的近似值，它表示属于预测块表示的宏块部分的所有样本的运动矢量选择。 理想情况下，每个示例都有其自己的运动向量，但这会消耗大量的位，需要额外的开销来处理。

预测块仅涉及一个宏块分区。 整个预测块涵盖了宏块的16x16 区域。  (这是所有261和 MPEG-2 预测的情况。 ) MPEG-2 引入了16x8 预测形状来处理 macroblocks 的双字段/帧性质。 还借用了16x8 形状，可用于 MPEG-2 字段结构化图片，以创建更精细的预测粒度。 8x8 形状部署在 (高级预测) 和 MPEG-2 中。 每个色度预测块通常都使用从相应亮度预测块的运动向量派生的运动向量，因为标准模型运动对于所有颜色组件都是相同的。

色度预测块通常大小为其相应亮度预测块的水平和垂直方向的一半。 因此，色度矢量通常是通过向下缩放亮度向量来得出的，以考虑各自亮度和色度样本维度中的差异。 MPEG 2's 16x8 亮度预测块具有相应的8x4 色度形状。

当亮度预测块太小时，通常会进行缩放色度块尺寸的异常。 例如，在 ".H 高级" 预测模式下，色度预测块在形状中仍为8x8，而色度运动矢量派生自四个8x8 亮度运动向量的缩放平均值。

 

 





