---
title: 在视频微型端口驱动程序中重置适配器
description: 在视频微型端口驱动程序中重置适配器
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，重置适配器
- 重置适配器 WDK 视频微型端口
- HwVidResetHw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a4c8264bb05cc1cd63e1d9f92e4e5e5227a349f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799607"
---
# <a name="resetting-the-adapter-in-video-miniport-drivers"></a>在视频微型端口驱动程序中重置适配器


## <span id="ddk_resetting_the_adapter_in_video_miniport_drivers_gg"></span><span id="DDK_RESETTING_THE_ADAPTER_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


如果无需重新启动计算机，则每个微型端口驱动程序都必须具有 [*HwVidResetHw*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_reset_hw) 函数。

如果计算机即将崩溃或用户启动计算机的软重启，则 *HAL* 会调用 *HwVidResetHw* 。 *HwVidResetHw* 将适配器重置为指定的字符模式，因此 HAL 可以显示崩溃转储信息，因为它会在软重启期间关闭系统或初始化信息。

*HwVidResetHw* 无法调用 BIOS，无法调用任何可分页的代码，也无法进行分页。 如果可能，它应只调用 **VideoPortRead**_xxx_ 和 **VideoPortWrite**_xxx_ 函数，但它也可以调用以下任一方法：

[**VideoPortStallExecution**](/windows-hardware/drivers/ddi/video/nf-video-videoportstallexecution)

[**VideoPortZeroDeviceMemory**](/windows-hardware/drivers/ddi/video/nf-video-videoportzerodevicememory)

[**VideoPortZeroMemory**](/windows-hardware/drivers/ddi/video/nf-video-videoportzeromemory)

 

