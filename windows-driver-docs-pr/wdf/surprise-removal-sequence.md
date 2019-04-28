---
title: 意外删除顺序
description: 意外删除顺序
ms.assetid: 5A89BEDA-BAC3-476F-99B3-4E6E6DDDE5F5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c90800119f063f7bf039e05346ff13c0b13a661
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350681"
---
# <a name="surprise-removal-sequence"></a>意外删除顺序


如果用户只需拔下它而无需使用设备管理器或安全删除硬件实用工具中删除而不发出警告，设备，设备被视为"意外删除。" 此操作时，framework 遵循略有不同的删除顺序。 如果另一个驱动程序调用意外删除序列还遵循[ **IoInvalidateDeviceState** ](https://msdn.microsoft.com/library/windows/hardware/ff549361)在设备上，即使设备仍以物理方式呈现。 在意外删除序列中，框架将调用[ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913)之前删除序列中调用任何其他回调的回调。 在序列完成后，框架将销毁设备对象。 所有可移动设备的驱动程序必须确保在关闭和启动路径中的回调可以处理失败，尤其是通过删除对硬件造成的故障。 任何尝试访问硬件不应无限期等待，但应该会有所超时或监视计时器。

下图显示在意外删除中所涉及的回调：

![surprise-removal sequence](images/surprise-removal.png)

如果设备当时不处于工作状态中，已将其删除时，框架将调用[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)事件回调后立即[ *EvtDeviceSurpriseRemoval*](https://msdn.microsoft.com/library/windows/hardware/ff540913)。 它会省略设备退出从工作状态时已执行的中间步骤。

 

 





