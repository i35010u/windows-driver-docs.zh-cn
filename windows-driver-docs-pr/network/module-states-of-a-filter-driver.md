---
title: 筛选器驱动程序的模块状态
description: 筛选器驱动程序的模块状态
ms.assetid: 139679d6-d3dc-433b-a35a-eb1e5ed3cb33
keywords:
- 筛选器驱动程序 WDK 网络、 模块状态
- NDIS 筛选器驱动程序 WDK，模块状态
- 模块状态 WDK 网络
- 筛选器模块 WDK 网络筛选器驱动程序的状态
- 筛选器驱动程序 WDK 网络筛选器模块
- NDIS 筛选器驱动程序 WDK，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60c2d6269ffbd9fb8f5ce53d6ea25f581ef26a6d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362322"
---
# <a name="module-states-of-a-filter-driver"></a>筛选器驱动程序的模块状态





[NDIS 筛选器驱动程序](ndis-filter-drivers.md)必须为每个驱动程序管理的筛选器模块 （实例的筛选器驱动程序） 支持以下操作状态：

-   Detached

-   附加

-   已暂停

-   重新启动

-   正在运行

-   暂停

下图显示了这些状态之间的关系。

![说明筛选器模块状态的关系图](images/filterstate.png)

以下定义的筛选器模块状态：

<a href="" id="detached"></a>分离  
*Detached*状态是筛选器模块的初始状态。 NDIS 此状态筛选器模块时，可以调用筛选器驱动程序[ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)函数来将筛选器模块附加到驱动程序堆栈。 当 NDIS 调用筛选器驱动程序*FilterAttach*函数，筛选器模块进入附加状态。 如果在附加操作失败，筛选器模块返回到已分离状态。 调用该模块时已暂停的状态和 NDIS [ *FilterDetach* ](https://msdn.microsoft.com/library/windows/hardware/ff549918)函数，该模块返回到已分离状态。

<a href="" id="attaching"></a>附加  
当筛选器模块处于*附加*状态中时，筛选器驱动程序正在准备将该模块附加到驱动程序堆栈。 筛选器模块准备已完成后，筛选器模块将进入暂停状态。 如果失败发生 （例如，因为所需的资源不可用），筛选器模块返回到已分离状态。

<a href="" id="paused"></a>已暂停  
当筛选器模块处于*已暂停*状态时，筛选器模块不会执行发送或接收操作。 当筛选器模块处于*附加*状态并[ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)是成功，将筛选器模块进入*已暂停*状态。 当筛选器模块处于*暂停*状态和暂停操作完成后，筛选器模块进入*已暂停*状态。 当筛选器模块处于*已暂停*状态和 NDIS 调用筛选器驱动程序[ **FilterRestart** ](https://msdn.microsoft.com/library/windows/hardware/ff549962)函数，筛选器模块进入*正在重新启动*状态。 当筛选器模块处于*已暂停*状态和 NDIS 调用驱动程序的*FilterDetach*处理程序中，筛选器模块进入*Detached*状态。

<a href="" id="restarting"></a>重新启动  
在中*正在重新启动*状态中时，筛选器驱动程序完成重启发送和接收操作的筛选器模块所需的任何操作。 当筛选器模块是处于已暂停状态时，NDIS 调用驱动程序的*FilterRestart*函数，筛选器模块进入正在重新启动状态。 如果在重新启动失败，筛选器模块将返回到暂停状态。 如果在重新启动成功，筛选器模块将进入运行状态。

<a href="" id="running"></a>运行  
在中*运行*状态中时，筛选器驱动程序执行正常发送和接收处理筛选器模块。 当筛选器模块处于正在重新启动状态，该驱动程序已准备好执行发送和接收操作时，筛选器模块将进入运行状态。

<a href="" id="pausing"></a>暂停  
在中*暂停*状态中时，筛选器驱动程序完成停止发送和接收操作的筛选器模块所需的任何操作。 筛选器驱动程序必须等待所有其未完成发送请求，以完成，并且 NDIS 以返回所有其未处理接收的指示。 当筛选器模块处于运行状态，NDIS 调用驱动程序的[ *FilterPause* ](https://msdn.microsoft.com/library/windows/hardware/ff549957)函数，筛选器模块将进入暂停状态。 筛选器驱动程序不能故障暂停操作。 暂停操作完成后，筛选器模块将进入暂停状态。

## <a name="related-topics"></a>相关主题


[驱动程序堆栈管理](driver-stack-management.md)

[NDIS 筛选器驱动程序](ndis-filter-drivers.md)

 

 






