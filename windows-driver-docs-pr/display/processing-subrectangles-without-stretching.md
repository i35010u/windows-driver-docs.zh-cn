---
title: 在不拉伸的情况下处理子矩形
description: 在不拉伸的情况下处理子矩形
keywords:
- 取消隔行扫描 WDK DirectX VA，subrectangular 处理
- subrectangular 处理 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cdbbea32a96dc0c77e6ea99e7718a07c02c879b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840753"
---
# <a name="processing-subrectangles-without-stretching"></a>在不拉伸的情况下处理子矩形


## <span id="ddk_processing_subrectangles_without_stretching_gg"></span><span id="DDK_PROCESSING_SUBRECTANGLES_WITHOUT_STRETCHING_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

在以下两个示例中，目标图面为 720 x 576，目标矩形的坐标为 {0,0,720,576} ，背景色为纯色。

第一个示例演示视频流和子流矩形不相交的情况。

在此示例中，引用视频流和单子流的特征体现如下：

-   视频流坐标：
    -   源图面： {0,0,720,480}
    -   源 subrectangle (**rcSrc**) ： {360,240,720,480}
    -   目标 subrectangle (**rcDest**) ： {0,0,360,240}
-   子流坐标：
    -   源图面： {0,0,640,576}
    -   源 subrectangle (**rcSrc**) ： {0,288,320,576}
    -   目标 subrectangle (**rcDest**) ： {400,0,720,288}

在此示例中，视频流的左下角显示在目标表面的左上角，子流的右下角将显示在目标图面的右上角上，。 下图显示了取消隔行扫描和子流组合操作的输出， (哈希区域指示) 处理的 subrectangles。

![说明不带交集处理 subrectangles 的关系图](images/trgrect5.png)

第二个示例演示视频流和子流矩形相交的情况。

在第二个示例中，源 surface 坐标与第一个示例中的坐标相同。 在此示例中，引用视频流和单子流的特征是以下 subrectangular 坐标：

-   视频流 subrectangular 坐标：
    -   源 subrectangle (**rcSrc**) ： {260,92,720,480}
    -   目标 subrectangle (**rcDest**) ： {0,0,460,388}
-   子流 subrectangular 坐标：
    -   源 subrectangle (**rcSrc**) ： {0,0,460,388}
    -   目标 subrectangle (**rcDest**) ： {260,188,720,576}

在此示例中，视频流的右下角显示在目标表面的左上角，并按 + 100 移动到 X 轴和 Y 轴上。 子流的左上角显示在目标图面的右下角，并在 X 和 Y 轴上移动-100。 下图显示了组合取消隔行扫描和子流组合操作的输出。

![演示如何处理 subrectangles 与交集的关系图](images/trgrect6.png)

 

 





