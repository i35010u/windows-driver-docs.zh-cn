---
title: 拉伸子矩形
description: 拉伸子矩形
keywords:
- 取消隔行扫描 WDK DirectX VA，subrectangular 处理
- subrectangular 处理 WDK DirectX VA
- 拉伸 WDK Windows 2000 显示器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eaf9ce2bfa147ee16e09923c143a24f995dd8f95
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813797"
---
# <a name="stretching-subrectangles"></a>拉伸子矩形


## <span id="ddk_stretching_subrectangles_gg"></span><span id="DDK_STRETCHING_SUBRECTANGLES_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

在下面的示例中，目标图面为 720 x 480，目标矩形的坐标为 {0,0,720,480} ，背景色为纯色。

视频流的源图面为 360 x 240，具有以下源和目标 subrectangles：

-   源 subrectangle (**rcSrc**) ： {180,120,360,240}

-   目标 subrectangle (**rcDest**) ： {0,0,360,240}

单个子流的源图面为 360 x 240，具有以下源和目标 subrectangles：

-   源 subrectangle (**rcSrc**) ： {0,0,180,120}

-   目标 subrectangle (**rcDest**) ： {360,240,720,480}

下图显示了组合取消隔行扫描和子流组合操作的输出。

![演示拉伸 subrectangles 的示意图](images/trgrect7.png)

 

 





