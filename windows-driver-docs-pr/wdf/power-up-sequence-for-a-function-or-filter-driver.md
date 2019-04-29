---
title: 函数或筛选器驱动程序的启动顺序
description: 函数或筛选器驱动程序的启动顺序
ms.assetid: 3E904641-A1E2-400C-A201-2D1D2D359657
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4d6093a9a544bf21eb829425f70374886985f41
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390056"
---
# <a name="power-up-sequence-for-a-function-or-filter-driver"></a>函数或筛选器驱动程序的启动顺序


下图显示了使设备为完全可操作的状态，从该图底部的设备插入状态时框架调用 KMDF 函数或筛选器驱动程序的事件回调函数的顺序：

![函数或筛选器驱动程序的设备枚举和增益道具序列](images/fdo-fido-powerup.png)

广泛的水平线将标记中启动设备所涉及的步骤。 图左侧列描述相应步骤，并在右侧列列出完成该操作的事件回调。

在该图底部，设备不存在系统上。 框架在用户插入设备，首先调用驱动程序的[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调，以便该驱动程序可以创建一个设备对象来表示该设备。 框架将继续进行向上访问序列，直到该设备正常调用驱动程序的回调例程。 请记住，框架会因此调用图中所示的自下而上的顺序中的事件回调[ *EvtDeviceFilterRemoveResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff540872)之前调用[ *EvtDeviceFilterAddResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff540870) ，依此类推。 如果设备已停止来重新平衡资源，或以物理方式存在，但在低功耗状态，并非所有的步骤是必需的如图所示。

 

 





