---
title: ITU-T H.263
description: ITU-T H.263
ms.assetid: 08926037-da17-4ab0-81c5-9fd78cb1133c
keywords:
- ITU-T H-p WDK DirectX VA
- H. WDK DirectX VA
- OBMC WDK DirectX VA
- INTER4V WDK DirectX VA
- 双向预测 WDK DirectX VA
- 运动向量 WDK DirectX VA
- 舍入控制 WDK DirectX VA
- 图片边界 WDK DirectX VA
- macroblocks WDK DirectX VA，ITU-T H-p
- PB 帧 WDK DirectX VA
- deblocking 筛选器 WDK DirectX VA
- 多个参考框架 WDK DirectX VA
- 逆离散-余弦转换 WDK DirectX VA
- IDCT WDK DirectX VA
- 独立段解码 WDK DirectX VA
- 降低-分辨率更新 WDK DirectX VA
- 参考图片重新采样 WDK DirectX VA
- 伸缩性 WDK DirectX VA
- 引用图片选择 WDK DirectX VA
- 预测块 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a663b477705973479de7ab025159cb088aeaebc
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361353"
---
# <a name="itu-t-h263"></a>ITU-T H.263


## <span id="ddk_itu_t_h_263_gg"></span><span id="DDK_ITU_T_H_263_GG"></span>


ITU-T 建议的 .H 标题为低比特率通信的视频编码。 此建议提供相对于261、MPEG-2 和 MPEG-2 的压缩性能改进。 .H 标准包含操作的基线模式，仅支持最基本的 H-p 功能。 它还包含大量可选的、增强的操作模式，可用于各种目的。 基线 H-p 预测使用 MPEG-2 功能的子集在此接口中运行。 基线模式不包含双向预测-ˆ ' 仅向前预测。

**舍入控制：** 几个 H-p 可选模式需要舍入控制。 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)的 **bRcontrol** 成员支持此功能。

**图片边界之上的运动矢量：** 几个 H-p 可选模式允许按照 .H 附录 D 中的定义，根据图片边界来寻址位置的运动矢量。 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)的 **bPicExtrapolation** 成员指示加速器是否需要支持此类动作。 加速器可以通过两种方式来支持图片边界上的运动矢量。 在任一情况下，结果均相同：

-   剪裁每个提取示例中地址的值，以确保其保持在图片边界内。

-   使用重复的示例填充图片，以将每个宏块宽度和高度使用的实际内存区扩大到图片的每个边框上。

**双向运动预测：** 在某些可选的 h-p 预测操作中使用的双向运动预测使用与 mpeg-2 不同的舍入运算符。  (它使用的是半整数值的向下舍入，而不是向上舍入。 ) [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)的 **bBidirectionalAveragingMode** 成员将指示用于在双向运动补偿中合并预测平面的舍入方法。

**4-MV 运动补偿 (INTER4V)** ：尽管宏块中的每个大小都为16x16， (例如，的附录 F 和附录) J，宏块允许为单个发送四个运动向量，并为宏块中的四个8x8 的每个亮度块发送一个运动矢量。 对应的8x8 色度区使用单个派生运动向量。

**重叠的块运动补偿 (OBMC)** ： .H 附录 F 包含重叠的块运动补偿 () OBMC 的亮度示例，以及 INTER4V 支持。 支持使用 OBMC 预测来发送12个运动向量，以便向前预测宏块。

OBMC 预测块可在硬件加速器中实现，作为分为三个平面的预测的组合：

-   当前平面 (其平面索引为零) 

-    (，其平面索引为 1) 

-    (的左/右平面，其平面索引为 2) 

这三个平面可以作为 *(x、y)* 、 *r (x、y)* 以及在-263 部分中定义的 *(x，y)* 的块 q 的临时存储。 在为所有四个块填充了三个平面后，可以根据中的公式，将它们与 .H 第3部分中的公式组合在一起，并根据在 H-p 附录 F 中给定的各自的 *H* 矩阵对它们进行加权。

例如，OBMC 亮度宏块预测可能由8个顶部/底部预测块组成：8x4 形状、8个左/右块、4x8 形状和四个当前8x8 块。 如果具有索引0的平面的所有四个运动向量都具有相同的运动向量 (也就是说，如果不在 INTER4V 宏块) 中，则可以使用单个16x16 宏块预测来填充整个16x16 平面。

为实现 DirectX VA 中的 OBMC 过程，将为宏块发送10个运动向量，如下图所示。 前四个运动矢量适用于当前宏块中的 Y ₀、Y ₁、Y ₂和 Y ₃块。 然后，按以下顺序发送远程运动向量：

1.  宏块顶部的左侧和右侧部分。

2.  宏块左侧的上半部分和下半部分。

3.  宏块右侧的上半部分和下半部分。

下图显示了使用 OBMC 处理时为宏块发送的运动矢量。  (字母 C 指示当前宏块的运动向量。 字母 R 指示与当前宏块相关的运动向量。 ) 

![说明在使用重叠的块运动补偿 (obmc) 处理时为宏块发送的十个运动向量的关系图](images/10vectors.png)

请注意，对于宏块底部的左侧和右侧，".H" 不使用不同的远程向量，它重用当前宏块的矢量。

下图显示了如何将一个8x8 块放置在 OBMC 处理的三种类型的预测平面中。

![说明在重叠的块运动补偿 (obmc) 预测平面中的一个8x8 块的 .h 注册的关系图](images/h263reg.png)

**(附录 G 和 M) 的 PB 帧** ：在此模式下，P 帧的 macroblocks 和 pseudoâˆ "B" 帧将被多路复用到唯一的 "PB 帧" 图片编码类型。 每个宏块的 B 部分都是从为宏块的 P 部分编码的信息中借用的： B 帧向前和向后运动向量是从 P 帧矢量进行缩放的，而重建的 P 帧宏块充当 B 部分的后向引用。 PB 帧仅包括 pseudoâˆ B 帧，因为每个宏块的后向预测只能引用包含在同一 PB 宏块中的重建 P 宏块。 但是，与传统的 B 帧语义一样，PB 帧内的 B 宏块可以引用前向引用帧中的任何位置。 后向引用的限制将创建较小的向后预测块形状 (如) 中所述。 在 DirectX VA 中支持 PB 帧，方法是将 PB 帧的 P 部分表示为 P 帧，将 PB 帧中的 B 部分表示为独立的 B-P 双向预测图片，其中包含具有两个运动向量的唯一的宏块类型。

**Deblocking 筛选器 (附录 J)** ：定义了特殊的命令来加速 Deblocking 筛选器，无论是在 [运动补偿预测](motion-compensated-prediction.md) 循环中使用附录 J 还是在循环外部使用，在 Deblocking 261 图片或基线图片时。 如果需要， *主机 CPU* 必须创建 deblocking 命令来观察块 (GOB) 或切片段边界的组。

**引用图片选择 (Annexes N 和 U)** ：使用每个预测块的 "图片索引选择" 字段，加速器支持多个引用框架。

**) 的可伸缩性 (附录 o** ：在 SNR 中指定时态、可伸缩性和空间的可伸缩性功能。在中，可以从 DirectX VA 到 mpeg-2 的8帧非常类似。 空间伸缩性需要 upsampling 下层参考图片，然后使用 upsampled 图片作为参考图片来编码增强层图片 (在所有其他方面，空间伸缩性本质上与信噪比和) 时态可伸缩性相同。 对于 .H，应将相应的双向平均舍入控件设置为 "下偏差平均"。  (MPEG-2 和 MPEG-2 使用向上偏差平均，而 H-p 使用向下偏差的平均值。 ) 

**引用图片 (附录 P) 重新采样** ：引用缓冲区重新采样支持此附录的简单形式。 对于附录 P 重新采样的高级窗体，作为参考框架的重新构造的帧必须通过外部方法重新采样，并存储为可通过加速器寻址的引用帧缓冲区。

**(附录 Q) 的减少-分辨率更新** ：目前不支持 h-p 降低分辨率更新模式，因为它具有异常的残留 upsampling 要求、不同形式的 deblocking 筛选器以及不同形式的高级预测 OBMC。 但是，当 deblocking 筛选器模式和高级预测模式处于非活动状态时，此接口中可以支持使用基于主机的 IDCT 处理的减少-分辨率更新模式操作。

**独立段解码 (附录 R)** ：没有对独立段边框的加速功能。 如果没有任何特殊处理 (例如，基线加上附录 R) ，则可以支持某些形式的附录 R。 需要图片段推断方式的附录 R 的窗体可以通过将每个段解码为图片来支持，然后从这些较小的图片构造完整的输出图片。

**IDCT (附录 W) ：** 此接口支持 IDCT 的附录 W 中指定的反离散余弦转换 () 。

**其他 H-p 可选功能：** 可以支持 H-p 的其他可选功能，而不会对 DirectX VA 设计产生任何影响。 例如，可以通过更改软件解码器轻松地处理 Annexes I、K、S 和 T，而不会对加速器产生任何影响。

 

