---
title: DeinterlaceBltEx 概述
description: DeinterlaceBltEx 概述
ms.assetid: ff487508-eb04-4d4d-9057-ed2d9ea273e0
keywords:
- DeinterlaceBltEx，关于 DeinterlaceBltEx
- VMR WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e731cc35014459ddbab52418ebb7b5b4507df1c1
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066466"
---
# <a name="overview-of-deinterlacebltex"></a>DeinterlaceBltEx 概述


## <span id="ddk_overview_of_deinterlacebltex_gg"></span><span id="DDK_OVERVIEW_OF_DEINTERLACEBLTEX_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

Windows Server 2003 SP1 及更高版本和 Windows XP SP2 及更高版本上的 VMR 可以启动对显示驱动程序的 [**DeinterlaceBltEx**](./dxva-deinterlacebobdeviceclass-deinterlacebltex.md) 函数的调用，以组合取消隔行扫描和子流组合操作。

Windows Server 2003 和 Windows XP SP1 上的 VMR 使用 DXVA 进行逐行转换或帧速率转换视频，并将视频输出到 RGB32 表面。 然后，VMR 使用 Direct3D 将视频 substreams 与视频图像合并。 换句话说，视频首先 deinterlaced、调整了大小，然后使用显示器驱动程序的 [**DeinterlaceBlt**](./dxva-deinterlacebobdeviceclass-deinterlaceblt.md) 函数将颜色空间转换为 Direct3D RGB32 render 目标。 然后，使用对显示器驱动程序的 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 函数的调用，视频 substreams 显示在生成的视频图像的顶部。

使用 *DeinterlaceBltEx* 而不是 *DeinterlaceBlt* 和 *D3dDrawPrimitives2* 组合后，可以在可用硬件上更有效地执行操作。

还可以通过渐进式视频和多个视频 substreams 调用 *DeinterlaceBltEx* 函数。 当 VMR 用于包含渐进式和交错视频组合的 DVD 播放时，可能会出现这种情况。 在这种情况下，驱动程序不应尝试对视频流进行隔行扫描，因为该流已经是连续的。 驱动程序应将视频流与任何给定 substreams 合并，并根据需要调整每个流的大小。

如果在驱动程序中实现 [**DeinterlaceBltEx**](./dxva-deinterlacebobdeviceclass-deinterlacebltex.md) 函数，则还必须实现原始的 [**DeinterlaceBlt**](./dxva-deinterlacebobdeviceclass-deinterlaceblt.md) 函数。 Windows Server 2003 SP1 及更高版本和 Windows XP SP2 及更高版本上的 VMR 可以启动对驱动程序的 *DeinterlaceBltEx* 或 *DeinterlaceBlt* 函数的调用;应用程序控制 VMR 使用的功能。

 

