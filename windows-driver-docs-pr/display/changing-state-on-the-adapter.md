---
title: 更改适配器上的状态
description: 更改适配器上的状态
ms.assetid: bf503a42-ac32-4d68-9ad9-afec69c5fe2a
keywords:
- 视频适配器状态更改 WDK 微型端口
- 指出 WDK 微型端口
- 适配器状态 WDK 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06d226350958bfc61be436f81e14dcf07e3908c1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370332"
---
# <a name="changing-state-on-the-adapter"></a>更改适配器上的状态


## <span id="ddk_changing_state_on_the_adapter_gg"></span><span id="DDK_CHANGING_STATE_ON_THE_ADAPTER_GG"></span>


微型端口驱动程序不得永久更改之前的适配器的状态及其[ *HwVidInitialize* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_initialize)调用例程。 微型端口驱动程序例程之前调用*HwVidInitialize*，如[ *HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)不应更改任何视频适配器的状态不必要地并且也不可以，永久更改任何视频适配器的状态。

虽然[ *HwVidFindAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)运行，HAL 具有的视频适配器的控件，因此它也可以在系统启动过程的早期阶段中写到屏幕的信息。 如果*HwVidFindAdapter*的尝试，以确定其适配器会影响适配器的状态，此例程应还原原始状态，因此，在返回从立即*HwVidFindAdapter* HAL 可以继续显示启动消息。

例如， [ *HwVidFindAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)应确定 DAC 类型的适配器的遵循[ *HwVidInitialize* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_initialize)函数，因为在进行此决定不影响是否微型端口驱动程序将会加载，但会永久更改该适配器的状态。

 

 





