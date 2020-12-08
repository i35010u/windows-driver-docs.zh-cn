---
title: Bob 反交错机制
description: Bob 反交错机制
keywords:
- bob 取消隔行扫描 WDK DirectX VA，机械
- 交错字段 WDK DirectX VA
- stride WDK DirectX VA
- 取消隔行扫描 WDK DirectX VA，bob，机制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39a6683964f5c049e29ace67245ee5bdbf4744c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810441"
---
# <a name="bob-deinterlacing-mechanics"></a>Bob 反交错机制


## <span id="ddk_bob_deinterlacing_mechanics_gg"></span><span id="DDK_BOB_DEINTERLACING_MECHANICS_GG"></span>


所有可以执行位块传输的图形适配器都可以执行简单的 bob 样式取消隔行扫描。 当图面包含两个交错字段时，可以重新解释图面的内存布局来隔离每个字段。 这是通过将原始表面的步幅加倍，并将曲面的高度除以半来实现的。 以这种方式隔离两个字段后，可以通过将各个字段拉伸到正确的框架高度来 deinterlaced 它们。

还可以应用其他水平拉伸或收缩来更正视频图像像素的纵横比。 显示驱动程序可以确定其对 DirectX 视频混合呈现器 (VMR) 执行此操作的能力。 单个字段的高度可以按行复制垂直拉伸，也可以通过筛选的 stretch 进行垂直拉伸。 如果使用了行复制方法，则生成的映像具有 blocky 的外观。 如果使用筛选的 stretch，则生成的图像可能具有略微模糊的外观。

下图显示了包含两个交错字段的视频图面。

![阐释包含两个交错字段的图面的内存布局的关系图](images/deinterlace.png)

如果视频示例包含两个交错字段，由 [**DXVA \_ SampleFormat**](/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_sampleformat)枚举的 **DXVA \_ SampleFieldInterleavedEvenFirst** 和 **DXVA \_ SampleFieldInterleavedOddFirst** 成员指定，则第二个字段的开始时间是使用 [**rtStart \_ rtEnd**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample)结构的 **DXVA** 成员和 **VideoSample** 成员计算的，如下所示：

 (**rtStart**  +  **rtEnd**) /2

第一个字段的结束时间是第二个字段的开始时间。

 

