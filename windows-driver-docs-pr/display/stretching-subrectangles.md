---
title: 拉伸 Subrectangles
description: 拉伸 Subrectangles
ms.assetid: c8642ea4-67e9-4a15-9636-8d7efbfd8c9e
keywords:
- 取消隔行扫描 WDK DirectX VA，subrectangular 处理
- subrectangular 处理 WDK DirectX VA
- 拉伸 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e2874ddb904f8f13a8cf979f93dd2e6104dabbb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542735"
---
# <a name="stretching-subrectangles"></a>拉伸 Subrectangles


## <span id="ddk_stretching_subrectangles_gg"></span><span id="DDK_STRETCHING_SUBRECTANGLES_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。**

在以下示例中，目标面是 720 x 480、 目标矩形的坐标{0,0,720,480}，和背景色为纯黑色。

视频流的源图面为 360 x 240，使用以下源和目标 subrectangles:

-   源 subrectangle (**rcSrc**): {180,120,360,240}

-   目标 subrectangle (**rcDest**): {0,0,360,240}

单个子流的源图面为 360 x 240，使用以下源和目标 subrectangles:

-   源 subrectangle (**rcSrc**): {0,0,180,120}

-   目标 subrectangle (**rcDest**): {360,240,720,480}

下图显示了组合去隔行和子流组合的情况下操作的输出。

![说明延伸 subrectangles 的关系图](images/trgrect7.png)

 

 





