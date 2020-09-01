---
title: 卸载视频硬件
description: 卸载视频硬件
ms.assetid: 31bea975-1c4b-4157-aec9-49bb7ad69cd0
keywords:
- 显示驱动程序 WDK Windows 2000，视频硬件卸载
- 视频硬件卸载 WDK Windows 2000 显示器
- 硬件卸载 WDK Windows 2000 显示器
- 卸载视频硬件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17e83bf1d2f250dcc850e1ec7232f37518d37a88
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067174"
---
# <a name="unloading-video-hardware"></a>卸载视频硬件


## <span id="ddk_unloading_video_hardware_gg"></span><span id="DDK_UNLOADING_VIDEO_HARDWARE_GG"></span>


当不再需要某个图面时，对 [**DrvDisableSurface**](/windows/desktop/api/winddi/nf-winddi-drvdisablesurface) 的 GDI 调用会通知显示驱动程序可以禁用为当前硬件设备 [**创建的图**](/windows/desktop/api/winddi/nf-winddi-drvenablesurface) 面。 驱动程序还必须释放 surface 使用的所有资源。

禁用该图面后，GDI 将调用 [**DrvDisablePDEV**](/windows/desktop/api/winddi/nf-winddi-drvdisablepdev) 来通知驱动程序，不再需要硬件设备。 然后，该驱动程序将释放在处理 [**DrvEnablePDEV**](/windows/desktop/api/winddi/nf-winddi-drvenablepdev)的过程中分配的所有内存和资源。

最后，通过调用 [**DrvDisableDriver**](/windows/desktop/api/winddi/nf-winddi-drvdisabledriver)禁用显示驱动程序。 驱动程序必须释放在 [**DrvEnableDriver**](/windows/desktop/api/winddi/nf-winddi-drvenabledriver) 期间分配的任何资源，并将视频硬件还原到其默认状态。 驱动程序从 *DrvDisableDriver* 函数返回后，GDI 将释放为驱动程序分配的内存，并从内存中删除驱动程序代码和数据。

下图显示了用于禁用视频硬件的 GDI 调用序列。

![说明如何禁用视频硬件的示意图](images/202-02.png)

 

