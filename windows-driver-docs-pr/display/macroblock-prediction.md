---
title: 宏块预测
description: 宏块预测
ms.assetid: 95e779ab-b110-4636-9475-6881dba89649
keywords:
- MCP WDK DirectX VA
- 运动补偿 WDK DirectX VA
- DirectX 视频加速 WDK Windows 2000 显示视频解码
- 视频加速 WDK DirectX，视频解码
- VA WDK DirectX，视频解码
- 解码视频 WDK DirectX va，因此宏块预测
- 视频解码 WDK DirectX va，因此宏块预测
- 宏块 WDK DirectX va，因此预测
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2452e2bc5027d89aee452a9a358442024ff1b8c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380422"
---
# <a name="macroblock-prediction"></a>宏块预测


## <span id="ddk_macroblock_prediction_gg"></span><span id="DDK_MACROBLOCK_PREDICTION_GG"></span>


宏块预测通过经过运动补偿预测 (MCP) 形成必须作为一系列离散的阶段完成，如以下图和步骤中所示：

![说明创建宏块预测通过经过运动补偿预测 (mcp) 的关系图](images/preddata.png)

创建宏块预测所涉及的以下四个步骤：

1.  窗体的参考框架

    引用框架是一个未压缩的图面，先前创建的上一张图片，解码或直接写入视频加速器未压缩的图面。

2.  提取引用块

    引用块不一定是预测块相同。 它很可能包含在预测中筛选阶段所需的额外示例。 除非在内存单元中执行每半示例筛选，16 x 16 半示例筛选宏块引用块都有通过 8 像素元素数据列包含 8 行的每个块的块 17 x 17 矩阵。 引用块的大小为两个预测块维度的函数和预测块的筛选器特性。 从在中使用的参考帧缓冲区中提取数据的块引用块必须引用[经过运动补偿预测](motion-compensated-prediction.md)(MCP)。

    **请注意**  引用块未定义的 DirectX VA，因为它可能具有反映维护图片缓冲区的特定于实现的方法的属性。

     

3.  筛选引用块以形成预测块

    引用块可能会以生成预测块的第三个阶段中进行筛选。

4.  将合并到窗体宏块预测的预测块

    合并一个或多个预测块以形成宏块示例的最后一个预测。 通过在一个或多个预测平面中的相应块之间的像素值求平均值和舍入到最接近的整数的每个 （如果小数数据为 0.5 或更高版本） 合并块。 合并 P 图块使用暂时最近以前我或 P 图块。 B 图块与最近以前和未来相结合，我或 P 图块。

下图显示视频解码创建宏块预测时可能出现的过程中的其他步骤。 （与实线块描述运动补偿过程，而使用点线块描述视频解码的其他方面。）

![说明的运动补偿预测块信号流关系图](images/sigflowmo3.png)

 

 





