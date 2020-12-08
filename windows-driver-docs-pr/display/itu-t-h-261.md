---
title: ITU-T H.261
description: ITU-T H.261
keywords:
- ITU-T 261 WDK DirectX VA
- H. 261 WDK DirectX VA
- 预测块 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 636278c848e498e6ea64931c9d0ab3b3d2f9070a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792987"
---
# <a name="itu-t-h261"></a>ITU-T H.261


## <span id="ddk_itu_t_h_261_gg"></span><span id="DDK_ITU_T_H_261_GG"></span>


此标准标题为 "视听 Services at px64 kbit/s" 的视频编解码器，"ITU-T 建议 261"。 此建议包含与其他视频编解码器标准相同的基本设计。 261对 Y、Cb 和 Cr 组件使用8位样本，4:2:0 采样，基于16x16 宏块的运动补偿，8x8 IDCT，基于0值运行长度和量化索引值的组合，系数的系数、标量量化和系数的可变长度编码。

所有261预测块使用上图中的只进预测。 261不具有半样本准确预测筛选器，而是使用一种名为 "循环筛选器" 的低传递筛选器，该筛选器) 261 规范的 "循环筛选器 (" 部分，可在每个宏块的运动补偿预测期间关闭或打开。

**附录 D 图形**

建议的261附录 D 图形传输模式可以通过将四个已解码的图片从该加速器上传回主机，并将其交错显示为更高分辨率的图形来支持。

 

 





