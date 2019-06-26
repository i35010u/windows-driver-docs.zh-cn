---
title: 视频微型端口驱动程序中的计时器
description: 视频微型端口驱动程序中的计时器
ms.assetid: 257ea76e-7be6-4895-8e83-0f50c96e5969
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，计时器
- 计时器 WDK 视频微型端口
- HwVidTimer
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 633464727896f2aa3e0c1d02975515a806525f8f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385656"
---
# <a name="timers-in-video-miniport-drivers"></a>视频微型端口驱动程序中的计时器


## <span id="ddk_timers_in_video_miniport_drivers_gg"></span><span id="DDK_TIMERS_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


任何视频微型端口驱动程序可以具有[ **HwVidTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_timer)裁量权的驱动程序编写器的函数。 一个*HwVidTimer*函数允许微型端口驱动程序超时操作，或用于监视状态更改粗粒度的间隔内不能通过调用[ **VideoPortStallExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportstallexecution). *HwVidTimer*也不会阻止发生与其他系统操作**VideoPortStallExecution** does。

例如，用于模拟 VGA 功能的适配器的微型端口驱动程序可能*HwVidTimer*定期将监视其适配器"VGA"状态的函数注册以便驱动程序可模拟 VGA 样式图形。

在调用[ **VideoPortStartTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportstarttimer)，视频端口驱动程序调用*HwVidTimer*一次微型端口驱动程序调用直到每隔一秒[ **VideoPortStopTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportstoptimer)。 微型端口驱动程序可以启用和禁用对调用*HwVidTimer*函数重复。

请注意， *HwVidTimer*函数不能禁用调用到其自身与**VideoPortStopTimer**。 另一个微型端口驱动程序函数必须控制启用或禁用的求助电话*HwVidTimer*使用函数**VideoPortStartTimer**和**VideoPortStopTimer**.

 

 





