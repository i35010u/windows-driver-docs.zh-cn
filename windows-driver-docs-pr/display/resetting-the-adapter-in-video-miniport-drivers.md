---
title: 在视频微型端口驱动程序中重置适配器
description: 在视频微型端口驱动程序中重置适配器
ms.assetid: 321a5b6c-5a70-4acb-bf88-42ffb0cff86d
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，重置适配器
- 重置适配器 WDK 视频微型端口
- HwVidResetHw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1b2755ed8ce36af4420eda8408b97b811a1fdc0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385660"
---
# <a name="resetting-the-adapter-in-video-miniport-drivers"></a>在视频微型端口驱动程序中重置适配器


## <span id="ddk_resetting_the_adapter_in_video_miniport_drivers_gg"></span><span id="DDK_RESETTING_THE_ADAPTER_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


每个微型端口驱动程序必须具有[ *HwVidResetHw* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_reset_hw)函数如果其适配器不能重置为未初始化状态而无需硬重新启动计算机。

*HwVidResetHw*由调用*HAL*如果即将损坏计算机或用户启动软重新启动计算机。 *HwVidResetHw*将适配器重置到指定的字符模式，因此 HAL 可以显示故障转储信息，如关闭软重启期间的系统或初始化信息。

*HwVidResetHw*不能调用 BIOS，不能调用任何可分页的代码，也不可能它会在可分页。 如果可能，它的调用应仅 **VideoPortRead * * * Xxx*和 **VideoPortWrite * * * Xxx*函数，但它还可以调用任意以下值：

[**VideoPortStallExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportstallexecution)

[**VideoPortZeroDeviceMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportzerodevicememory)

[**VideoPortZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportzeromemory)

 

 





