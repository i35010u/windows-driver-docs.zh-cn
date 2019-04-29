---
title: DeinterlaceBltEx 概述
description: DeinterlaceBltEx 概述
ms.assetid: ff487508-eb04-4d4d-9057-ed2d9ea273e0
keywords:
- DeinterlaceBltEx，有关 DeinterlaceBltEx
- VMR WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 461f99398f6bc2efc32cc7cdc201236ae80262c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383985"
---
# <a name="overview-of-deinterlacebltex"></a>DeinterlaceBltEx 概述


## <span id="ddk_overview_of_deinterlacebltex_gg"></span><span id="DDK_OVERVIEW_OF_DEINTERLACEBLTEX_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。**

在 Windows Server 2003 SP1 及更高版本的 VMR 和 Windows XP SP2 和更高版本可以启动对显示驱动程序调用[ **DeinterlaceBltEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563927)函数合并去隔行和组合的情况下的子流操作。

在 Windows Server 2003 和 Windows XP SP1 VMR 使用 DXVA 来取消隔行扫描或帧速率转换视频并输出到 RGB32 图面上的视频。 VMR 然后使用 Direct3D 视频子流结合视频图像。 换而言之，首先 deinterlaced 视频，调整大小和颜色空间转换到 Direct3D RGB32 然后呈现目标使用显示器驱动程序的[ **DeinterlaceBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff563924)函数。 然后，视频子流都是复合使用对显示驱动程序的调用生成的视频图像上方[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)函数。

通过使用*DeinterlaceBltEx*而非*DeinterlaceBlt*并*D3dDrawPrimitives2*结合使用，可以执行操作更高效地在可用的硬件.

*DeinterlaceBltEx*还可以使用渐进式视频和多个视频的子流调用函数。 VMR 用于混合的渐进式和交错视频的 DVD 播放时，则会出现此情况。 在这种情况下，该驱动程序不应尝试取消隔行扫描视频流，因为该流已渐进式。 该驱动程序应将视频流与任何给定的子流相结合，并调整大小所需的每个流。

如果你实现了[ **DeinterlaceBltEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563927)函数在您的驱动程序，您还必须实现原始[ **DeinterlaceBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff563924)函数。 在 Windows Server 2003 SP1 及更高版本的 VMR 和 Windows XP SP2 和更高版本可以启动调用为驱动程序的*DeinterlaceBltEx*或*DeinterlaceBlt*函数; 该应用程序控制的函数 VMR 使用。

 

 





