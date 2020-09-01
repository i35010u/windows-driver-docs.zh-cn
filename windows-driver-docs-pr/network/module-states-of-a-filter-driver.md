---
title: 筛选器驱动程序的模块状态
description: 筛选器驱动程序的模块状态
ms.assetid: 139679d6-d3dc-433b-a35a-eb1e5ed3cb33
keywords:
- 筛选器驱动程序 WDK 网络，模块状态
- NDIS 筛选器驱动程序 WDK，模块状态
- 模块状态 WDK 网络
- 筛选器模块 WDK 网络，筛选器驱动程序的状态
- 筛选器驱动程序 WDK 网络，筛选器模块
- NDIS 筛选器驱动程序 WDK，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba5fcc9baf7c3c199b73cd6bcf46b0f8703a2c8c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215556"
---
# <a name="module-states-of-a-filter-driver"></a>筛选器驱动程序的模块状态





[NDIS 筛选器驱动程序](ndis-filter-drivers.md)必须支持驱动程序管理) 的每个筛选器模块 (实例的下列操作状态：

-   分离

-   附加

-   已暂停

-   重新启动

-   正在运行

-   正在暂停

下图显示了这些状态之间的关系。

![阐释筛选器模块状态的关系图](images/filterstate.png)

下面定义了筛选器模块状态：

<a href="" id="detached"></a>分离  
*分离*状态是筛选器模块的初始状态。 当筛选器模块处于此状态时，NDIS 可以调用筛选器驱动程序的 [*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach) 函数将筛选器模块附加到驱动程序堆栈。 当 NDIS 调用筛选器驱动程序的 *FilterAttach* 函数时，筛选器模块将进入附加状态。 如果附加操作失败，筛选器模块将返回到已分离状态。 当模块处于暂停状态并且 NDIS 调用 [*FilterDetach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach) 函数时，该模块将返回到已分离状态。

<a href="" id="attaching"></a>附加  
当筛选器模块处于 *附加* 状态时，筛选器驱动程序准备将模块附加到驱动程序堆栈。 筛选器模块准备完成后，筛选器模块将进入暂停状态。 如果发生了失败 (例如，因为所需的资源) 不可用，则筛选器模块将返回到已分离状态。

<a href="" id="paused"></a>悬停  
当筛选器模块处于 *暂停* 状态时，筛选器模块不执行发送或接收操作。 如果筛选器模块处于 *附加* 状态并且 [*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach) 成功，则筛选器模块将进入 *暂停* 状态。 如果筛选器模块处于 *暂停* 状态并且暂停操作完成，则筛选器模块将进入 *暂停* 状态。 当筛选器模块处于 *暂停* 状态，并且 NDIS 调用筛选器驱动程序的 [**FilterRestart**](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_restart) 函数时，筛选器模块将进入 *重新启动* 状态。 如果筛选器模块处于 *暂停* 状态，并且 NDIS 调用驱动程序的 *FilterDetach* 处理程序，则筛选器模块将进入已 *分离* 状态。

<a href="" id="restarting"></a>重新启动  
在 *重新启动* 状态下，筛选器驱动程序完成为筛选器模块重新启动发送和接收操作所需的任何操作。 当筛选器模块处于暂停状态并且 NDIS 调用驱动程序的 *FilterRestart* 函数时，筛选器模块将进入重新启动状态。 如果重启失败，筛选器模块将返回到 "已暂停" 状态。 如果重新启动成功，筛选器模块将进入 "正在运行" 状态。

<a href="" id="running"></a>耗尽  
在 " *正在运行* " 状态下，筛选器驱动程序将执行筛选器模块的正常发送和接收处理。 当筛选器模块处于重新启动状态并且驱动程序已准备好执行发送和接收操作时，筛选器模块将进入 "正在运行" 状态。

<a href="" id="pausing"></a>暂停  
在 *暂停* 状态下，筛选器驱动程序完成为筛选器模块停止发送和接收操作所需的任何操作。 筛选器驱动程序必须等待所有未完成的发送请求完成，NDIS 才能返回所有未完成的接收指示。 当筛选器模块处于运行状态，并且 NDIS 调用驱动程序的 [*FilterPause*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause) 函数时，筛选器模块将进入暂停状态。 筛选器驱动程序不能使暂停操作失败。 暂停操作完成后，筛选器模块将进入暂停状态。

## <a name="related-topics"></a>相关主题


[驱动程序堆栈管理](driver-stack-management.md)

[NDIS 筛选器驱动程序](ndis-filter-drivers.md)

 

