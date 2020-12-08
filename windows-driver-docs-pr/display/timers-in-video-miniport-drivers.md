---
title: 视频微型端口驱动程序中的计时器
description: 视频微型端口驱动程序中的计时器
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，定时器
- 计时器音频视频微型端口
- HwVidTimer
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8763589698c464f53701c87fdfc6249c66215b9c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836489"
---
# <a name="timers-in-video-miniport-drivers"></a>视频微型端口驱动程序中的计时器


## <span id="ddk_timers_in_video_miniport_drivers_gg"></span><span id="DDK_TIMERS_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


任何视频微型端口驱动程序都可以使用 [**HwVidTimer**](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_timer) 函数来决定驱动程序编写器。 使用 *HwVidTimer* 函数，可以使微型端口驱动程序超时操作，也可以通过调用 [**VideoPortStallExecution**](/windows-hardware/drivers/ddi/video/nf-video-videoportstallexecution)来监视粒度较粗的间隔内的状态更改。 *HwVidTimer* 也不会阻止其他系统操作，因为 **VideoPortStallExecution** 会出现这种情况。

例如，模拟 VGA 功能的适配器的微型端口驱动程序可能有一个 *HwVidTimer* 函数，该函数会定期监视其适配器的 "VGA" 注册的状态，以便驱动程序可以模拟 VGA 样式的图形。

调用 [**VideoPortStartTimer**](/windows-hardware/drivers/ddi/video/nf-video-videoportstarttimer)后，视频端口驱动程序每秒调用 *HwVidTimer* 一次，直到视频微型端口驱动程序调用 [**VideoPortStopTimer**](/windows-hardware/drivers/ddi/video/nf-video-videoportstoptimer)。 视频微型端口驱动程序可以重复启用和禁用对 *HwVidTimer* 函数的调用。

请注意， *HwVidTimer* 函数不能禁用对 **VideoPortStopTimer** 的调用。 另一个视频微型端口驱动程序函数必须通过使用 **VideoPortStartTimer** 和 **VideoPortStopTimer** 控制对 *HwVidTimer* 函数的调用的启用或禁用。

 

