---
title: 宏块分区
description: 宏块分区
ms.assetid: 8b21df67-0f59-4c6d-8db6-f7ff7c982587
keywords:
- 解码视频 WDK DirectX va，因此宏块预测
- 视频解码 WDK DirectX va，因此宏块预测
- 宏块 WDK DirectX va，因此预测
- 色度预测阻止 WDK DirectX VA
- 预测阻止 WDK DirectX VA
- 宏块 WDK DirectX va，因此分区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 018f8dea3a87ff1d07c6498a4a57efe6cd5e9d98
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380427"
---
# <a name="macroblock-partitioning"></a>宏块分区


## <span id="ddk_macroblock_partitioning_gg"></span><span id="DDK_MACROBLOCK_PARTITIONING_GG"></span>


宏块可以分为以下段。 （这是以分隔具有不同特征的区域。）下图显示了如何使可分为以下段。

![说明分区方案的基本宏块的关系图](images/portschem.png)

MPEG 2 种情况下，在帧图片结构字段的宏块的顶部和底部部分从不同的实例在时间，最多一个-fiftieth 相隔第二个捕获的两个不同字段表示行。 因此，如果宏块所覆盖的帧区域的两个字段之间已发生重大移动的顶部和底部的部分可以具有完全非相关内容。 下图中所示，结构字段的图片，以提供更好地适应边缘和较小的对象具有不同的动作特征预测的更细的垂直粒度中添加其他的 16 x 8 方案。

![关系图演示两个 mpeg-2 宏块 16 x 8 分区](images/m2macro.png)

预测块本身是形状的近似值，代表属于预测块代表宏块的一部分的所有示例的动作矢量泄漏所选内容。 理想情况下，每个示例将具有其自己的动作矢量，但这会占用相当长的比特数，并且要求在处理过程中的额外开销。

预测块会导致宏块的只有一个分区。 整个预测块介绍宏块的 16x16 区域。 （这是与所有 H.261 和 mpeg-1 预测的情况）。MPEG 2 引入了 16 x 8 预测形状中，以解决块效应的双字段/框架特性。 16 x 8 形状也已在 mpeg-2 结构字段的图片以创建更细的粒度的预测中使用借用。 8 x 8 形状部署在 H.263 （高级预测） 和 MPEG 4。 每个色度预测块通常使用派生自相应的亮度预测块，motion 向量的动作矢量，因为标准模型的所有颜色组件相同动作。

色度预测块通常具有在水平和垂直方向上的其对应的亮度预测块的大小的一半。 因此通过减少亮度向量的各自的亮度和色度示例维度中的差异通常派生色度向量。 MPEG-2 16 x 8 亮度预测块包含相应 8 x 4 色度形状。

亮度预测块变得太小时通常设置为缩放色度块维度的方法例外。 例如，在 H.263 高级预测模式下，色度预测块将保留在形状中，8 x 8 和色度动作矢量派生自四个 8 x 8 亮度运动向量的缩放平均值。

 

 





