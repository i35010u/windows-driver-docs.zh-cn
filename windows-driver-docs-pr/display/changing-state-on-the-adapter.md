---
title: 更改适配器上的状态
description: 更改适配器上的状态
keywords:
- 视频适配器状态更改 WDK 视频微型端口
- 状态 WDK 视频微型端口
- 适配器状态 WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de72ddbc4a6d4156250644f952cb2a5fe03aa17c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810327"
---
# <a name="changing-state-on-the-adapter"></a>更改适配器上的状态


## <span id="ddk_changing_state_on_the_adapter_gg"></span><span id="DDK_CHANGING_STATE_ON_THE_ADAPTER_GG"></span>


小型端口驱动程序不能永久更改适配器的状态，直到调用其 [*HwVidInitialize*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize) 例程为止。 在 *HwVidInitialize* 之前调用的微型端口驱动程序例程（如 [*HwVidFindAdapter*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)）不会不必要地更改任何视频适配器的状态，也不能永久更改任何视频适配器的状态。

当 [*HwVidFindAdapter*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter) 运行时，HAL 控制视频适配器，因此它可以在系统启动过程的早期阶段将信息写入屏幕。 如果 *HwVidFindAdapter* 尝试识别适配器的状态，则此例程应立即还原原始状态，以便在 *HwVidFindAdapter* 上返回时，HAL 可以继续显示启动消息。

例如， [*HwVidFindAdapter*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter) 应延迟将适配器的 DAC 类型确定为 [*HwVidInitialize*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize) 函数，因为进行此确定不会影响是否将加载微型端口驱动程序，而是永久更改适配器的状态。

 

