---
title: ITU-T H.261
description: ITU-T H.261
ms.assetid: 00fb9001-2896-4ecd-b6ee-5b36bc6e72cd
keywords:
- ITU T H.261 WDK DirectX VA
- H.261 WDK DirectX VA
- 预测阻止 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f66f4242a3db24e27de5fbfdc50de2dbfecad9d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362091"
---
# <a name="itu-t-h261"></a>ITU-T H.261


## <span id="ddk_itu_t_h_261_gg"></span><span id="DDK_ITU_T_H_261_GG"></span>


此标准的标题为"视听服务 px64 为/秒，视频编解码器"ITU-T 建议 H.261。 此建议包含稍后在其他视频编解码器标准中使用相同的基本设计。 H.261 使用 8 位样本 Y、 Cb 和 Cr 组件，4:2:0 采样，16x16 宏块基于运动补偿 8x8 IDCT 之字形反系数、 标量量化和可变长度编码基于的组合的系数个数的扫描零值的运行长度和量化索引值。

所有 H.261 预测块都使用只进预测从上一张图片。 H.261 不具有半示例准确预测的筛选器，而是使用一种名为可以打开或关闭在每个宏块的运动补偿预测过程的循环筛选器 （H.261 规范的第 3.2.3 部分） 的低通滤波器。

**Annex D 图形**

可以通过读取回到主机上的加速器四个已解码的图片和作为分辨率更高的图形图片显示在它们存在交错执行支持建议 H.261 Annex D 图传输模式。

 

 





