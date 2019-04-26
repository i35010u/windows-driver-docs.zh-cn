---
title: 将高度和宽度不同的两个流合并
description: 将高度和宽度不同的两个流合并
ms.assetid: a4b0e32d-17f0-4373-bed2-ce9248b3ceb2
keywords:
- 组合流式传输 WDK DirectX VA
- 视频流结合使用 WDK DirectX VA
- 流结合使用 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 763a1186579773c932f05f067130d6aaa0f89ee6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329858"
---
# <a name="combining-two-streams-with-different-heights-and-widths"></a>将高度和宽度不同的两个流合并


## <span id="ddk_combining_two_streams_with_different_heights_and_widths_gg"></span><span id="DDK_COMBINING_TWO_STREAMS_WITH_DIFFERENT_HEIGHTS_AND_WIDTHS_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。

在以下示例中，VMR 调用使用视频流和视频可以具有不同高度和宽度的驱动程序。 下图显示了如何操作，请在此示例中，该驱动程序结合了两个流和背景色：

![说明将与具有不同高度和宽度的两个流结合使用背景色的关系图](images/trgrect3.png)

请注意，在前面的示例驱动程序的**DeinterlaceBltEx**函数应仅指定的背景色上绘制目标矩形中，如以下关系图中所示。

![说明减少输出图像的大小的关系图](images/trgrect4.png)

在前面的示例中，VMR 定向到原来的两个水平和垂直减少输出图像的大小。 仅应目标矩形中显示的背景色。 该驱动程序必须向目标图面中的像素的目标矩形 （在上图中影线） 之外写入内容。 在前面的示例中，目标面为 300 x 200 像素，但目标矩形是 {0，0,150,100}。 为视频流的源矩形{0,0,300,150}; 视频流的目标矩形是{0,12,150,87}。 子流源矩形是{0,0,150,200}; 子流目标矩形是 {37,0,112，100}。 请记住，目标矩形的边框的视频流，以及所有子流。

 

 





