---
title: 帧结构化图片
description: 帧结构化图片
keywords:
- MPEG-2 WDK DirectX VA
- 帧运动补偿 WDK DirectX VA
- 现场 (16x8) 运动补偿 WDK DirectX VA
- 双重运动补偿 WDK DirectX VA
- 16x8 运动补偿 WDK DirectX VA
- 预测块 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6b112a380974335ef5acd98cce86839c69e30a9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799680"
---
# <a name="frame-structured-pictures"></a>帧结构化图片


## <span id="ddk_frame_structured_pictures_gg"></span><span id="DDK_FRAME_STRUCTURED_PICTURES_GG"></span>


**帧 MC**：帧运动补偿具有16x16 预测块形状，与 mpeg-2 预测类似。 这是由 MPEG-2) 中的 *运动 \_ 类型* 变量指定的 mpeg-2 (中唯一的渐进式动作补偿。 有一个 *预测平面* (仅向前或向后) ，或者两个 (双向) ，它们由 *宏块 \_ 类型* mpeg-2 变量确定。 引用块是从帧缓冲区中的连续帧系列组成的。 帧缓冲区由解码过程的语义选择。 半示例内插 (MPEG-2 节 7.6.4) 和双向内插 (MPEG-4 节 7.6.7.1) 的平均运算方式与 MPEG-2 大小写相同。

**现场 (16x8) MC**： field (16x8) 运动补偿具有每个预测平面 (向前和向后方向) 包含 top 16x8 预测块和底部16x8 预测块。 与每个预测块相对应的引用块可以从引用帧的顶部字段或底部字段中提取，如 mpeg-2 可变 *动作 \_ 垂直 \_ 字段 \_* 所确定 \[ *r* \] \[ *s* \] 。 现场 (16x8) 的运动补偿有两种可能：

-   一个预测平面的两个预测块的一组 (向前或向后仅针对每个宏块) 两个预测块的预测。

-   两组两个预测平面的两组 (双向预测，在宏块) 中使用四个预测块。

**双质数 MC**：类似于现场 (16x8) 运动补偿，双质数运动补偿具有 (奇偶校验的每个平面，) 由顶部和底部16x8 形状组成。 相同和相反的奇偶校验平面在求平均值运算中组合在一起。 此平均运算与用于 MPEG-2 中其他运动类型的双向内插完全相同。 与其他运动补偿类型不同，双重质数宏块始终包含两组预测块 (相同且相反的奇偶校验) ，每个宏块总共四个预测块。

 

 





