---
title: 将高度和宽度不同的两个流合并
description: 将高度和宽度不同的两个流合并
keywords:
- 合并流 WDK DirectX VA
- 视频流组合 WDK DirectX VA
- 流组合 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27b508a65d05aa55d33655dbdfc452f3650e2007
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810277"
---
# <a name="combining-two-streams-with-different-heights-and-widths"></a>将高度和宽度不同的两个流合并


## <span id="ddk_combining_two_streams_with_different_heights_and_widths_gg"></span><span id="DDK_COMBINING_TWO_STREAMS_WITH_DIFFERENT_HEIGHTS_AND_WIDTHS_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

在下面的示例中，VMR 使用视频流和不同高度的视频子流和宽度来调用驱动程序。 下图显示了在此示例中，驱动程序如何合并两个流和背景色：

![说明如何将背景色与不同高度和宽度的两个流结合使用的关系图](images/trgrect3.png)

请注意，在前面的示例中，驱动程序的 **DeinterlaceBltEx** 函数只应在目标矩形上绘制指定的背景色，如下图所示。

![阐释如何减小输出图像的大小的关系图](images/trgrect4.png)

在前面的示例中，对 VMR 进行定向以将输出图像的大小水平和垂直减小一倍。 背景色只应显示在目标矩形中。 驱动程序不得写入目标矩形之外的目标图面中的像素， (上图) 中的阴影。 在前面的示例中，目标图面为300x200 像素，但目标矩形为 {0，0150100}。 视频流的源矩形为 {0,0,300,150} ; 视频流的目标矩形为 {0,12,150,87} 。 子流源矩形为 {0,0,150,200} ; 子流目标矩形为 {37，0112，100}。 请记住，目标矩形是视频流和所有 substreams 的边框。

 

 





