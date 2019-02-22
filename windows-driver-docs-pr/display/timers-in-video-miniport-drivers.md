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
ms.openlocfilehash: 87fe04e53916866dc27ef9cc36436ffc3f987a37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547581"
---
# <a name="timers-in-video-miniport-drivers"></a>视频微型端口驱动程序中的计时器


## <span id="ddk_timers_in_video_miniport_drivers_gg"></span><span id="DDK_TIMERS_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


任何视频微型端口驱动程序可以具有[ **HwVidTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff567371)裁量权的驱动程序编写器的函数。 一个*HwVidTimer*函数允许微型端口驱动程序超时操作，或用于监视状态更改粗粒度的间隔内不能通过调用[ **VideoPortStallExecution**](https://msdn.microsoft.com/library/windows/hardware/ff570368). *HwVidTimer*也不会阻止发生与其他系统操作**VideoPortStallExecution** does。

例如，用于模拟 VGA 功能的适配器的微型端口驱动程序可能*HwVidTimer*定期将监视其适配器"VGA"状态的函数注册以便驱动程序可模拟 VGA 样式图形。

在调用[ **VideoPortStartTimer**](https://msdn.microsoft.com/library/windows/hardware/ff570370)，视频端口驱动程序调用*HwVidTimer*一次微型端口驱动程序调用直到每隔一秒[ **VideoPortStopTimer**](https://msdn.microsoft.com/library/windows/hardware/ff570371)。 微型端口驱动程序可以启用和禁用对调用*HwVidTimer*函数重复。

请注意， *HwVidTimer*函数不能禁用调用到其自身与**VideoPortStopTimer**。 另一个微型端口驱动程序函数必须控制启用或禁用的求助电话*HwVidTimer*使用函数**VideoPortStartTimer**和**VideoPortStopTimer**.

 

 





