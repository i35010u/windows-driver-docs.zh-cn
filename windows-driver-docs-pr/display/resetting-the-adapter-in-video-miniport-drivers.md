---
title: 重置视频微型端口驱动程序中的适配器
description: 重置视频微型端口驱动程序中的适配器
ms.assetid: 321a5b6c-5a70-4acb-bf88-42ffb0cff86d
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，重置适配器
- 重置适配器 WDK 视频微型端口
- HwVidResetHw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54ac4ce9ab3a43f62ab736928ca12fc608427525
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526239"
---
# <a name="resetting-the-adapter-in-video-miniport-drivers"></a>重置视频微型端口驱动程序中的适配器


## <span id="ddk_resetting_the_adapter_in_video_miniport_drivers_gg"></span><span id="DDK_RESETTING_THE_ADAPTER_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


每个微型端口驱动程序必须具有[ *HwVidResetHw* ](https://msdn.microsoft.com/library/windows/hardware/ff567363)函数如果其适配器不能重置为未初始化状态而无需硬重新启动计算机。

*HwVidResetHw*由调用*HAL*如果即将损坏计算机或用户启动软重新启动计算机。 *HwVidResetHw*将适配器重置到指定的字符模式，因此 HAL 可以显示故障转储信息，如关闭软重启期间的系统或初始化信息。

*HwVidResetHw*不能调用 BIOS，不能调用任何可分页的代码，也不可能它会在可分页。 如果可能，它的调用应仅 **VideoPortRead * * * Xxx*和 **VideoPortWrite * * * Xxx*函数，但它还可以调用任意以下值：

[**VideoPortStallExecution**](https://msdn.microsoft.com/library/windows/hardware/ff570368)

[**VideoPortZeroDeviceMemory**](https://msdn.microsoft.com/library/windows/hardware/ff570492)

[**VideoPortZeroMemory**](https://msdn.microsoft.com/library/windows/hardware/ff570493)

 

 





