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
ms.openlocfilehash: 7cf8e145bd97bf94c452d602bcbcdc669f2c3660
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838442"
---
# <a name="security-issues-for-section-objects-and-views"></a>节对象和视图的安全问题





如果创建的部分和视图不与用户模式共享，则这些驱动程序必须在使用以下协议时使用以下协议：

-   驱动程序在打开 section 对象的句柄时必须使用内核句柄。 驱动程序可以确保句柄是内核句柄，方法是在系统进程中创建它，或指定该句柄的 OBJ\_内核\_句柄属性。 有关详细信息，请参阅[对象句柄](object-handles.md)。

-   视图必须仅从系统线程映射。 （否则，视图可以从在其中创建它的上下文中访问。）驱动程序可以通过使用系统工作线程执行映射操作，确保视图从系统进程映射。 有关详细信息，请参阅[系统工作线程](system-worker-threads.md)和[驱动程序线程上下文](driver-thread-context.md)。

与用户模式进程共享视图的驱动程序必须在使用以下协议时使用以下协议：

-   驱动程序而不是用户模式进程，必须创建节对象并映射视图。

-   如前所述，驱动程序在打开 section 对象的句柄时必须使用内核句柄。 驱动程序可以确保句柄是内核句柄，方法是在系统进程中创建它，或指定该句柄的 OBJ\_内核\_句柄属性。 有关详细信息，请参阅[对象句柄](object-handles.md)。

-   视图映射到共享视图的进程的线程上下文中。 最高级别的驱动程序可以通过在调度例程（如[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)）中执行映射操作来保证在当前进程上下文中映射视图。 较低级别驱动程序的调度例程在任意线程上下文中运行，因此不能安全地映射调度例程中的视图。 有关详细信息，请参阅[驱动程序线程上下文](driver-thread-context.md)。

-   对驱动程序中视图的所有内存访问都必须通过**尝试**-**例外块除外**。 恶意用户模式应用程序可以取消对视图的映射或更改视图的保护状态。 否则将导致系统崩溃，除非受到-**除块以外**的**尝试**。 有关详细信息，请参阅[处理异常](handling-exceptions.md)。

驱动程序还必须根据需要验证视图的内容。 驱动程序编写器无法假定只有受信任的用户模式组件可以访问该视图。

必须将节对象与用户模式应用程序共享的驱动程序（该应用程序必须能够创建其自己的视图）才能使用以下协议：

-   驱动程序而不是用户模式进程必须创建节对象。 驱动程序绝不能使用从用户模式传递的句柄。

-   在将句柄传递给用户模式之前，驱动程序必须调用[**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)来获取对节对象的引用。 这可以防止恶意应用程序通过关闭句柄来删除节对象。 对象引用应存储在驱动程序的设备扩展中。

-   驱动程序不再使用 section 对象之后，必须调用[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)来释放对象引用。

在运行 Microsoft Windows Server 2003 Service Pack 1 （SP1）和更高版本的系统上，只有内核模式驱动程序可以打开 \\**设备**\\**PhysicalMemory**。 但是，驱动程序可以决定向用户应用程序分配一个句柄。 若要防止安全问题，只应为驱动程序信任的用户应用程序授予对 \\**设备**的访问权限\\**PhysicalMemory**。

 

 




