---
title: 运动补偿预测
description: 运动补偿预测
keywords:
- MCP WDK DirectX VA
- 运动补偿 WDK DirectX VA
- DirectX 视频加速 WDK Windows 2000 显示，视频解码
- 视频加速 WDK DirectX，视频解码
- VA WDK DirectX，视频解码
- 解码视频 WDK DirectX VA，运动补偿预测
- 视频解码 WDK DirectX VA，运动补偿预测
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4a1b55eb2407a3b6fb6678147d007a52942a3b4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838493"
---
# <a name="motion-compensated-prediction"></a>运动补偿预测


## <span id="ddk_motion_compensated_prediction_gg"></span><span id="DDK_MOTION_COMPENSATED_PREDICTION_GG"></span>


阻塞运动-补偿预测 (MCP) 是 DirectX VA 实现的预测类型。 这种预测类型为 llap 能够大幅系列编解码器的优点优于纯静止帧编码方法，如 JPEG。 DirectX VA 不实现除基于块的预测以外的运动补偿预测类型。

在运动补偿预测中，以前传输和解码的数据将用作当前数据的预测。 预测误差和实际当前数据值之间的差异。 将编码的预测错误添加到预测以获取输入数据的最终表示形式。 将编码的预测错误添加到 MCP 后，MCP 中将使用最终解码图片来生成后续编码的图片。

这种递归循环偶尔会由特定于所预测元素的各种重置类型中断。 重置是通过解码过程的语义来描述的。  (例如，运动向量和系数预测在切片边界重置，而整个时态帧预测链将由内部刷新帧重置。 ) 

下图显示了用于运动补偿预测的信号流。

![说明运动补偿预测信号流的示意图](images/sigflow.png)

图片的动画补偿预测编码所需的步骤如下所示：

1.  将从以前解码的帧中提取引用块，并按编码模式选择的指定修改引用块，并将其修改为构成每个图像块的预测。

2.  当前输入数据块与预测之间经过转换的差异在编码器的可用比特率范围内大致近似，并以编码预测错误的形式发送。

3.  预测和反向转换的预测错误都进行了求和，形成了一个重建图片块。

4.  重新构造的图片块存储在引用帧缓冲区中，用于预测后续图片。

5.  此过程将在步骤1中再次继续。

运动矢量、DCT 系数和其他不属于 MCP 流程的数据也会运用预测来更紧凑地传输数据形式。 这些预测实例在 *主机 CPU* 处理器或位流分析器/可变长度解码单元上执行。

 

 





