---
title: 节对象和视图的安全问题
description: 节对象和视图的安全问题
ms.assetid: a2044ea1-c90c-4487-850b-d07ac55aea6d
keywords:
- 内存段 WDK 内核
- 节对象 WDK 内核
- 查看 WDK 内存部分
- 安全 WDK 内存部分
- 协议 WDK 内存部分
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48880d6502ab1c537d7b97b4826690aba8d6f585
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185273"
---
# <a name="security-issues-for-section-objects-and-views"></a>节对象和视图的安全问题





如果创建的部分和视图不与用户模式共享，则这些驱动程序必须在使用以下协议时使用以下协议：

-   驱动程序在打开 section 对象的句柄时必须使用内核句柄。 驱动程序可以确保句柄是内核句柄，只需在系统进程中创建它，或指定 \_ 句柄的 OBJ 内核 \_ 句柄属性即可。 有关详细信息，请参阅 [对象句柄](object-handles.md)。

-   视图必须仅从系统线程映射。 否则 (可以从在其中创建该视图的上下文的进程中访问该视图。 ) 驱动程序可以通过使用系统工作线程执行映射操作来确保从系统进程中映射视图。 有关详细信息，请参阅 [系统工作线程](system-worker-threads.md) 和 [驱动程序线程上下文](driver-thread-context.md)。

与用户模式进程共享视图的驱动程序必须在使用以下协议时使用以下协议：

-   驱动程序而不是用户模式进程，必须创建节对象并映射视图。

-   如前所述，驱动程序在打开 section 对象的句柄时必须使用内核句柄。 驱动程序可以确保句柄是内核句柄，只需在系统进程中创建它，或指定 \_ 句柄的 OBJ 内核 \_ 句柄属性即可。 有关详细信息，请参阅 [对象句柄](object-handles.md)。

-   视图映射到共享视图的进程的线程上下文中。 最高级别的驱动程序可以通过在调度例程（如 [*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)）中执行映射操作来保证在当前进程上下文中映射视图。 较低级别驱动程序的调度例程在任意线程上下文中运行，因此不能安全地映射调度例程中的视图。 有关详细信息，请参阅 [驱动程序线程上下文](driver-thread-context.md)。

-   **try** - **除了块外**，必须先保护驱动程序内对该视图的所有内存访问。 恶意用户模式应用程序可以取消对视图的映射或更改视图的保护状态。 否则会导致系统崩溃，除非由**try** - **except**块保护。 有关详细信息，请参阅 [处理异常](handling-exceptions.md)。

驱动程序还必须根据需要验证视图的内容。 驱动程序编写器无法假定只有受信任的用户模式组件可以访问该视图。

必须与用户模式应用程序共享 section 对象的驱动程序， (必须能够创建其自己的视图) 必须使用以下协议：

-   驱动程序而不是用户模式进程必须创建节对象。 驱动程序绝不能使用从用户模式传递的句柄。

-   在将句柄传递给用户模式之前，驱动程序必须调用 [**ObReferenceObjectByHandle**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle) 来获取对节对象的引用。 这可以防止恶意应用程序通过关闭句柄来删除节对象。 对象引用应存储在驱动程序的设备扩展中。

-   驱动程序不再使用 section 对象之后，必须调用 [**ObDereferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject) 来释放对象引用。

在运行 Microsoft Windows Server 2003 Service Pack 1 (SP1) 及更高版本的系统上，只有内核模式驱动程序可以打开 \\ **设备** \\ **PhysicalMemory**。 但是，驱动程序可以决定向用户应用程序分配一个句柄。 若要防止安全问题，只应为驱动程序信任的用户应用程序提供对 \\ **设备** \\ **PhysicalMemory**的访问权限。

 

