---
title: 丢失驱动程序管理的纹理
description: 丢失驱动程序管理的纹理
ms.assetid: 19f87190-bb3a-40a6-a216-8df9816e2842
keywords:
- 绘图图面 WDK DirectDraw，丢失的纹理
- DirectDraw 面，WDK Windows 2000 显示，丢失的纹理
- WDK DirectDraw，丢失纹理的图面
- 挂起的纹理 WDK DirectDraw
- 纹理 WDK DirectDraw 丢失
- 丢失的纹理 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09546d6cc08c3d567299ca92dbfc429b528c9212
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380411"
---
# <a name="losing-driver-managed-textures"></a>丢失驱动程序管理的纹理


## <span id="ddk_losing_driver_managed_textures_gg"></span><span id="DDK_LOSING_DRIVER_MANAGED_TEXTURES_GG"></span>


驱动程序管理纹理图面，使用视频内存，需要能够放置在挂起状态 （丢失）。 因为驱动程序控制的驱动程序管理纹理表面的视频内存分配，方法会通知驱动程序时需要通过扩展到丢失这种纹理图面[ *DdDestroySurface*](https://msdn.microsoft.com/library/windows/hardware/ff549281)调用。

当驱动程序管理纹理图面 (标有 DDSCAPS2\_TEXTUREMANAGE 标志) 是丢失，驱动程序收到一个特殊*DdDestroySurface*使用 DDRAWISURF 调用\_中指定的无效**dwFlags**纹理图面上结构中的成员。 驱动程序应释放托管的纹理图面，与关联的视频内存，但不是应释放任何其他私人图面上信息包括支持 （系统内存） 映像的视频内存副本的图面。 会有任何新[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)调用，以还原丢失的驱动程序管理纹理图面，因为它们不会真正丢失从驱动程序的角度来看。 大多数情况下，此特殊*DdDestroySurface*调用用来通知该驱动程序，它应逐出其视频内存副本。

 

 





