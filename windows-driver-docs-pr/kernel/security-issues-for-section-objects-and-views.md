---
title: 节对象和视图的安全问题
description: 节对象和视图的安全问题
ms.assetid: a2044ea1-c90c-4487-850b-d07ac55aea6d
keywords:
- 内存部分 WDK 内核
- 部分对象 WDK 内核
- 视图 WDK 内存部分
- 安全 WDK 内存部分
- 协议 WDK 内存部分
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 818231039bb7ca11c95e473fc9d4baf21d1cc53b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342697"
---
# <a name="security-issues-for-section-objects-and-views"></a>节对象和视图的安全问题





使用部分和视图时，驱动程序的创建部分，并将不与用户模式下共享的视图必须使用以下协议：

-   它打开部分对象的句柄时，该驱动程序必须使用内核句柄。 驱动程序可以确保句柄是内核句柄通过创建系统进程中，或者指定 OBJ\_内核\_句柄的句柄属性。 有关详细信息，请参阅[对象处理](object-handles.md)。

-   只能从某个系统线程都必须映射视图。 （否则，该视图是可从进程中创建其上下文中访问。）驱动程序可以确保视图通过使用系统工作线程来执行映射操作映射从系统进程。 有关详细信息，请参阅[系统工作线程数](system-worker-threads.md)并[驱动程序的线程上下文](driver-thread-context.md)。

使用部分和视图时，使用用户模式进程共享视图的驱动程序必须使用以下协议：

-   驱动程序不是用户模式下的过程，必须创建部分对象和映射视图。

-   前面曾提到，驱动程序必须使用内核句柄，它打开部分对象的句柄时。 驱动程序可以确保句柄是内核句柄通过创建系统进程中，或者指定 OBJ\_内核\_句柄的句柄属性。 有关详细信息，请参阅[对象处理](object-handles.md)。

-   视图映射中共享该视图的进程的线程上下文。 最高级别的驱动程序可以保证该视图当前进程上下文中映射通过执行映射操作中的调度例程，此类[ *DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)。 调度例程的较低级驱动程序运行在任意线程上下文中，并因此无法安全地映射中的调度例程的视图。 有关详细信息，请参阅[驱动程序的线程上下文](driver-thread-context.md)。

-   要在驱动程序中查看的所有内存访问必须都受**尝试**-**除**块。 恶意用户模式应用程序无法取消映射视图或更改视图的保护状态。 除非受会导致系统崩溃**尝试**-**除**块。 有关详细信息，请参阅[处理异常](handling-exceptions.md)。

该驱动程序还必须验证根据需要对视图的内容。 驱动程序编写器不能假定仅受信任的用户模式组件将有权访问视图。

必须使用用户模式应用程序 （即必须能够创建其自己的视图） 共享部分对象的驱动程序必须使用以下协议：

-   驱动程序不是用户模式下的过程，必须创建部分对象。 驱动程序必须永远不会使用从用户模式传递的句柄。

-   然后再将该句柄传递到用户模式下，该驱动程序必须调用[ **ObReferenceObjectByHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff558679)以获取对部分对象的引用。 这可以防止通过关闭句柄删除节对象的恶意应用程序。 对象引用应存储在驱动程序的设备扩展。

-   该驱动程序不再使用的部分对象后，它必须调用[ **ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)来释放该对象引用。

只将内核模式驱动程序可以在运行 Microsoft Windows Server 2003 Service Pack 1 (SP1) 和更高版本的系统，打开\\**设备**\\**PhysicalMemory**。 但是，驱动程序可以决定向用户应用程序的一个句柄。 若要防止出现安全问题，只有用户应用程序应提供了驱动程序的信任权\\**设备**\\**PhysicalMemory**。

 

 




