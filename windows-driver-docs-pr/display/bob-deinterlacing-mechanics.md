---
title: Bob 反交错机制
description: Bob 反交错机制
ms.assetid: 1735f9c6-ac83-4a6a-bc6f-4d4a193876dd
keywords:
- bob 取消隔行扫描 WDK DirectX VA，机械
- 交错字段 WDK DirectX VA
- stride WDK DirectX VA
- 取消隔行扫描 WDK DirectX VA，bob，机制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b36cf638e9cf03e4a092c54fd84be1eceb2f37a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839066"
---
# <a name="bob-deinterlacing-mechanics"></a>Bob 反交错机制


## <span id="ddk_bob_deinterlacing_mechanics_gg"></span><span id="DDK_BOB_DEINTERLACING_MECHANICS_GG"></span>


所有可以执行位块传输的图形适配器都可以执行简单的 bob 样式取消隔行扫描。 当图面包含两个交错字段时，可以重新解释图面的内存布局来隔离每个字段。 这是通过将原始表面的步幅加倍，并将曲面的高度除以半来实现的。 以这种方式隔离两个字段后，可以通过将各个字段拉伸到正确的框架高度来 deinterlaced 它们。

还可以应用其他水平拉伸或收缩来更正视频图像像素的纵横比。 显示驱动程序可以确定其对 DirectX 视频混合呈现器（VMR）执行此操作的能力。 单个字段的高度可以按行复制垂直拉伸，也可以通过筛选的 stretch 进行垂直拉伸。 如果使用了行复制方法，则生成的映像具有 blocky 的外观。 如果使用筛选的 stretch，则生成的图像可能具有略微模糊的外观。

下图显示了包含两个交错字段的视频图面。

![阐释包含两个交错字段的图面的内存布局的关系图](images/deinterlace.png)

如果视频示例包含两个交错字段，由**DXVA\_SampleFieldInterleavedEvenFirst**和**DXVA\_SampleFieldInterleavedOddFirst**成员指定[**DXVA\_SampleFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_sampleformat)枚举下，第二个字段的开始时间是使用[**DXVA\_VideoSample**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample)结构的**rtStart**和**rtEnd**成员进行计算的，如下所示：

（**rtStart** + **rtEnd**）/2

第一个字段的结束时间是第二个字段的开始时间。

 

 





