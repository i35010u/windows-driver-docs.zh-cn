---
title: 框架对象生命周期
description: 框架对象生命周期
ms.assetid: 33efc3a8-ac46-4626-ba0f-beb1eaa9ee47
keywords:
- framework 对象 WDK KMDF、 生命周期
- 生命周期 WDK KMDF
- framework 对象 WDK KMDF，创建
- 引用计数 WDK KMDF
- framework 对象 WDK KMDF，删除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31db062268fc2f45dffd6fb0c1889bbbd4308df3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370889"
---
# <a name="framework-object-life-cycle"></a>框架对象生命周期





Framework 对象的"生命周期"时被删除时，创建一个对象到跨越的时间。 对象的引用计数控件时它将被删除。

### <a name="creating-a-framework-object"></a>创建框架对象

由驱动程序的调用对象的创建方法创建框架的大多数对象。 例如，每个框架驱动程序必须调用[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)创建 framework 驱动程序对象。

由框架创建其他框架对象。 例如，当用户应用程序打开设备的读取或写入操作，框架创建框架文件对象并将其传递给驱动程序的[ *EvtDeviceFileCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff540868)回调函数。

可以创建几个 framework 对象，由任一框架或由驱动程序。 例如，当 I/O 管理器将 I/O 请求传递到驱动程序，框架将创建一个框架请求对象和将其传递给该驱动程序，通常通过调用一个驱动程序的请求处理程序。 驱动程序还可以创建 framework 请求对象并将其交付给其他驱动程序。

### <a name="using-reference-counts"></a>使用引用计数

框架维护每个对象的引用计数。 创建对象后，框架将设置其引用计数为 1。 如果引用计数变为零，框架将删除对象。

驱动程序可以通过调用修改对象的引用计数[ **WdfObjectReference** ](https://msdn.microsoft.com/library/windows/hardware/ff548758)递增引用计数或[ **WdfObjectDereference**](https://msdn.microsoft.com/library/windows/hardware/ff548739)要递减引用计数。 (驱动程序可以调用**WdfObjectDereference**仅当它以前被称为**WdfObjectReference**。)

在大多数情况下，驱动程序没有要递增或递减对象的引用计数。 框架增加计数传递对象的句柄到之前的驱动程序，和它递减计数时，驱动程序不再需要该对象。

驱动程序调用[ **WdfObjectReference** ](https://msdn.microsoft.com/library/windows/hardware/ff548758)以确保对象将不会删除 （通过该框架或由驱动程序线程） 之前该驱动程序使用完。 有关驱动程序应调用在其中出现示例情况**WdfObjectReference**并[ **WdfObjectDereference**](https://msdn.microsoft.com/library/windows/hardware/ff548739)，请参阅[发送的同步取消请求](synchronizing-cancellation-of-sent-requests.md)。

### <a name="deleting-a-framework-object"></a>正在删除 Framework 对象

对象是删除由于一个驱动程序调用[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)或因为框架将调用一个内部删除例程，但仅当其引用计数为零时删除对象。 驱动程序或框架已尝试删除对象后，该对象的句柄后仍保持有效直到引用计数变为零。 驱动程序*不能*只需调用删除对象[ **WdfObjectDereference** ](https://msdn.microsoft.com/library/windows/hardware/ff548739)以减少对象的引用计数为零-驱动程序还必须调用**WdfObjectDelete**。

如果框架对象是父级的子对象，则删除的父级，框架将尝试删除父级之前删除的子对象。 对象删除从距离最远的父对象开始，直至根对象层次结构向上工作原理。

驱动程序可以注册框架时，驱动程序或框架删除某个对象调用以下两个回调函数：

-   [ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)框架调用，以便该驱动程序可以调用的回调函数[ **WdfObjectDereference** ](https://msdn.microsoft.com/library/windows/hardware/ff548739)如果以前调用过[ **WdfObjectReference** ](https://msdn.microsoft.com/library/windows/hardware/ff548758)正在删除的对象。

-   [ *EvtDestroyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540841)回调函数，该框架将调用对象的引用计数后已减为零。

这些回调函数之一必须解除分配时创建对象时，该驱动程序分配给任何特定于对象的资源。

该框架将始终处理的某些 framework 对象，删除和驱动程序不得尝试删除这些对象。 无法删除驱动程序的 framework 对象的列表，请参阅[ **WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)。

 

 





