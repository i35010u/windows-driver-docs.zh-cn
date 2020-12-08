---
title: 卸载视频硬件
description: 卸载视频硬件
keywords:
- 显示驱动程序 WDK Windows 2000，视频硬件卸载
- 视频硬件卸载 WDK Windows 2000 显示器
- 硬件卸载 WDK Windows 2000 显示器
- 卸载视频硬件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3ca1b87ae0c8bdd3519bd9496e77b658f896028
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802555"
---
# <a name="unloading-video-hardware"></a>卸载视频硬件


## <span id="ddk_unloading_video_hardware_gg"></span><span id="DDK_UNLOADING_VIDEO_HARDWARE_GG"></span>


当不再需要某个图面时，对 [**DrvDisableSurface**](/windows/win32/api/winddi/nf-winddi-drvdisablesurface) 的 GDI 调用会通知显示驱动程序可以禁用为当前硬件设备 [**创建的图**](/windows/win32/api/winddi/nf-winddi-drvenablesurface) 面。 驱动程序还必须释放 surface 使用的所有资源。

禁用该图面后，GDI 将调用 [**DrvDisablePDEV**](/windows/win32/api/winddi/nf-winddi-drvdisablepdev) 来通知驱动程序，不再需要硬件设备。 然后，该驱动程序将释放在处理 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev)的过程中分配的所有内存和资源。

最后，通过调用 [**DrvDisableDriver**](/windows/win32/api/winddi/nf-winddi-drvdisabledriver)禁用显示驱动程序。 驱动程序必须释放在 [**DrvEnableDriver**](/windows/win32/api/winddi/nf-winddi-drvenabledriver) 期间分配的任何资源，并将视频硬件还原到其默认状态。 驱动程序从 *DrvDisableDriver* 函数返回后，GDI 将释放为驱动程序分配的内存，并从内存中删除驱动程序代码和数据。

下图显示了用于禁用视频硬件的 GDI 调用序列。

![说明如何禁用视频硬件的示意图](images/202-02.png)

 

