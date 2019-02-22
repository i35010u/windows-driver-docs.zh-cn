---
title: 处理 Subrectangles 而不是拉伸
description: 处理 Subrectangles 而不是拉伸
ms.assetid: ee59b06c-a3fb-41ac-875e-754d20a5eaa6
keywords:
- 取消隔行扫描 WDK DirectX VA，subrectangular 处理
- subrectangular 处理 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82740d69a5af194bbd2feca611988b2205e41a6c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555664"
---
# <a name="processing-subrectangles-without-stretching"></a>处理 Subrectangles 而不是拉伸


## <span id="ddk_processing_subrectangles_without_stretching_gg"></span><span id="DDK_PROCESSING_SUBRECTANGLES_WITHOUT_STRETCHING_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。**

在以下两个示例中，目标面是 720 x 576、 目标矩形的坐标{0,0,720,576}，和背景色为纯黑色。

第一个示例演示视频流和子流矩形不会相交的用例。

在此示例中，引用视频流和单个子流的特征体现在以下的矩形坐标：

-   视频流坐标：
    -   源面： {0,0,720,480}
    -   源 subrectangle (**rcSrc**): {360,240,720,480}
    -   目标 subrectangle (**rcDest**): {0,0,360,240}
-   坐标的子流：
    -   源面： {0,0,640,576}
    -   源 subrectangle (**rcSrc**): {0,288,320,576}
    -   目标 subrectangle (**rcDest**): {400,0,720,288}

在此示例中，视频流的左下角显示在目标面上，在左上角和子流在右下角显示目标面右上角。 下图显示了 （经过哈希处理的区域表示处理 subrectangles） 组合去隔行和子流组合的情况下操作的输出。

![说明不相交的情况下处理 subrectangles 的关系图](images/trgrect5.png)

第二个示例显示在其中的视频流和子流矩形相交的情况。

在第二个示例中，源图面上坐标中的第一个示例相同。 在此示例中，引用视频流和单个子流的特征体现在以下 subrectangular 坐标：

-   视频流 subrectangular 坐标：
    -   源 subrectangle (**rcSrc**): {260,92,720,480}
    -   目标 subrectangle (**rcDest**): {0,0,460,388}
-   子流 subrectangular 坐标：
    -   源 subrectangle (**rcSrc**): {0,0,460,388}
    -   目标 subrectangle (**rcDest**): {260,188,720,576}

在此示例中，视频流的右下角显示的左上角的目标图面，+ 100 X 和 Y 轴上移动。 子流在左上角显示的右下角的目标表面-100 X 和 Y 轴上移动。 下图显示了组合去隔行和子流组合的情况下操作的输出。

![说明与交集处理 subrectangles 的关系图](images/trgrect6.png)

 

 





