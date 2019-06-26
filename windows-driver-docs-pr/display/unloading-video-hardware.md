---
title: 卸载视频硬件
description: 卸载视频硬件
ms.assetid: 31bea975-1c4b-4157-aec9-49bb7ad69cd0
keywords:
- 显示驱动程序 WDK Windows 2000 中，视频硬件卸载
- 视频硬件卸载 WDK Windows 2000 显示
- 硬件卸载 WDK Windows 2000 显示
- 正在卸载视频硬件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfa7f47616d7556c506af4c114f7902cc2b0e840
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353400"
---
# <a name="unloading-video-hardware"></a>卸载视频硬件


## <span id="ddk_unloading_video_hardware_gg"></span><span id="DDK_UNLOADING_VIDEO_HARDWARE_GG"></span>


当图面不再是必需的 GDI 调用[ **DrvDisableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)告知表面的当前硬件设备创建的显示驱动程序[ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)可禁用。 该驱动程序还必须释放在图面时使用的任何资源。

禁用在图面后，调用 GDI [ **DrvDisablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)通知不再需要该硬件设备驱动程序。 该驱动程序然后释放任何内存和处理期间分配的资源[ **DrvEnablePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)。

最后，GDI 禁用显示器驱动程序通过调用[ **DrvDisableDriver**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledriver)。 该驱动程序必须释放期间分配的任何资源[ **DrvEnableDriver** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver)和视频硬件还原为其默认状态。 从驱动程序返回后*DrvDisableDriver*函数，GDI 释放它已经分配了驱动程序并从内存中删除驱动程序代码和数据的内存。

下图显示了用于禁用视频硬件 GDI 的调用序列。

![说明禁用视频硬件的关系图](images/202-02.png)

 

 





