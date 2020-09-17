---
title: 丢失驱动程序管理的纹理
description: 丢失驱动程序管理的纹理
ms.assetid: 19f87190-bb3a-40a6-a216-8df9816e2842
keywords:
- 绘图图面 WDK DirectDraw，丢失纹理
- DirectDraw 图面，WDK Windows 2000 显示，丢失纹理
- 显示 WDK DirectDraw，纹理丢失
- 暂停纹理 WDK DirectDraw
- 纹理 WDK DirectDraw，丢失
- 丢失纹理 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec26cdb202588e9c687a8efff0b4675985945ea3
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716272"
---
# <a name="losing-driver-managed-textures"></a>丢失驱动程序管理的纹理


## <span id="ddk_losing_driver_managed_textures_gg"></span><span id="DDK_LOSING_DRIVER_MANAGED_TEXTURES_GG"></span>


驱动程序管理的纹理图面（使用视频内存）需要功能处于挂起状态， (丢失) 。 由于驱动程序控制驱动程序托管纹理图面的视频内存分配，因此当需要通过 [*DdDestroySurface*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface) 调用的扩展来丢失此类纹理图面时，方法会通知驱动程序。

当使用 DDSCAPS2 TEXTUREMANAGE 标志 (标记的驱动程序托管纹理图面 \_) 丢失时，驱动程序将收到一个特殊的 *DdDestroySurface* 调用，其中 DDRAWISURF \_ 在纹理表面结构的 **dwFlags** 成员中指定了无效。 驱动程序应释放与托管纹理图面关联的视频内存，但不应释放任何其他专用表面信息，包括该图面的视频内存副本的支持 (系统内存) 映像。 由于驱动程序的观点并不真正丢失，因此不会有任何新的 [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)) 调用来还原丢失的驱动程序托管纹理图面。 大多数情况下，此特殊的 *DdDestroySurface* 调用用于通知驱动程序它应逐出其视频内存副本。

 

