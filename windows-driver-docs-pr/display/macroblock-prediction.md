---
title: 宏块预测
description: 宏块预测
keywords:
- MCP WDK DirectX VA
- 运动补偿 WDK DirectX VA
- DirectX 视频加速 WDK Windows 2000 显示，视频解码
- 视频加速 WDK DirectX，视频解码
- VA WDK DirectX，视频解码
- 解码视频 WDK DirectX VA，宏块预测
- 视频解码 WDK DirectX VA，宏块预测
- macroblocks WDK DirectX VA，预测
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1769f21fd23ffc743e46c0d955d4ad52eb771bc8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793929"
---
# <a name="macroblock-prediction"></a>宏块预测


## <span id="ddk_macroblock_prediction_gg"></span><span id="DDK_MACROBLOCK_PREDICTION_GG"></span>


宏块预测通过运动补偿预测 (MCP) 必须作为一系列离散阶段完成，如下图所示：

![说明如何通过运动补偿预测创建宏块预测 (mcp) ](images/preddata.png)

以下四个步骤涉及创建宏块预测：

1.  形成引用框架

    参考框架是先前图片的解码或直接写入视频加速器未压缩的图面上之前创建的未压缩图面。

2.  提取引用块

    引用块不必与预测块相同。 它最有可能包含预测筛选阶段中所需的额外示例。 除非在内存单元中执行了半示例筛选，否则16x16 半样本筛选后的宏块的引用块具有块的17x17 矩阵，其中每个块都包含8行 x 8 行的像素元素数据列。 引用块的大小既是预测块维度的函数，也是预测块的筛选器特性。 引用块必须引用从引用帧缓冲区中提取的数据块，以便在 (MCP) 的 [运动补偿预测](motion-compensated-prediction.md) 中使用。

    **注意**   未为 DirectX VA 定义引用块，因为它可能具有反映特定于实现的方式来维护图片缓冲区的属性。

     

3.  筛选引用块以形成预测块

    可以在第三个阶段筛选引用块以生成预测块。

4.  合并预测块以形成宏块预测

    将一个或多个预测块组合起来构成了宏块示例的最终预测。 通过对一个或多个预测平面中相应块之间的像素值进行求平均值，并将每个块向上舍入到最接近的整数 (当小数据为0.5 或更高) 时。 P picture 块与最近的暂时最近的 I 或 P 图片块合并在一起。 B 图片块与最近的、未来的 I 或 P 图片块组合在一起。

下图显示了在创建宏块预测时所发生的视频解码过程中的其他步骤。  (带有实线的块，说明运动补偿过程，而具有虚线的块则描述视频解码的其他方面。 ) 

![阐释运动补偿预测块的信号的示意图](images/sigflowmo3.png)

 

 





