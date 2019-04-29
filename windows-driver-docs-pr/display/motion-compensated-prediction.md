---
title: 运动补偿预测
description: 运动补偿预测
ms.assetid: 02706369-2d99-4ac9-8dad-9e431acff42f
keywords:
- MCP WDK DirectX VA
- 运动补偿 WDK DirectX VA
- DirectX 视频加速 WDK Windows 2000 显示视频解码
- 视频加速 WDK DirectX，视频解码
- VA WDK DirectX，视频解码
- 解码视频 WDK DirectX va，因此运动补偿预测
- 视频解码 WDK DirectX va，因此运动补偿预测
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e21f0a8336ceab731cbc881f5866487a58c0251
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354260"
---
# <a name="motion-compensated-prediction"></a>运动补偿预测


## <span id="ddk_motion_compensated_prediction_gg"></span><span id="DDK_MOTION_COMPENSATED_PREDICTION_GG"></span>


块经过运动补偿预测 (MCP) 是一种由 DirectX 弗吉尼亚实现预测 这种预测类型会使编解码器的 MPEG 和 H.26x 系列通过纯静止帧编码方法，如 JPEG 的优点。 经过运动补偿非基于块的预测的预测类型未实现的 DirectX 弗吉尼亚

在经过运动补偿预测中，以前传输和解码后的数据用作当前数据的预测。 预测和实际的当前数据值之间的区别是，预测误差。 编码的预测错误添加到预测来获取输入数据的最终表示形式。 编码的预测错误添加到 MCP 后，最终的已解码的图片用于在 MCP 生成后续编码的图片。

此递归循环有时是各种类型的特定于要预测的元素的重置的损坏。 重置介绍解码过程的语义。 （例如，动作矢量和系数预测会重置切片边界在整个临时帧预测链置内刷新帧时。）

下图显示了经过运动补偿预测的信号流。

![说明经过运动补偿预测信号流关系图](images/sigflow.png)

经过运动补偿预测的图片编码所需的步骤如下所示：

1.  引用块是从以前已解码的帧中提取并修改指定的编码的模式选择和动作矢量和其他预测命令以形成每个图块的预测。

2.  当前的输入的数据块和预测之间的转换后的区别近似等效于尽可能中可用的比特率编码器，并作为编码的预测误差发送结果。

3.  预测和逆转换预测误差求和以形成重新构造的图块。

4.  要用于后续图片的预测的参考帧缓冲区中存储的重新构造的图块。

5.  此过程将再次继续在步骤 1。

动作矢量、 DCT 系数和其他不直接是 MCP 的一部分的数据还处理采用预测，以使传输的形式的数据更紧凑。 预测这些实例上执行*承载 CPU*处理器或位流分析器/变量的长度解码单元。

 

 





