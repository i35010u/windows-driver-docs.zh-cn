---
title: 框架对象生命周期
description: 框架对象生命周期
keywords:
- framework 对象 WDK KMDF、生命周期
- 生命周期 WDK KMDF
- framework 对象 WDK KMDF，创建
- 引用计数 WDK KMDF
- framework 对象 WDK KMDF，删除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06e9c2fe26cbeb7c9eee320945a85815e385001d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815665"
---
# <a name="framework-object-life-cycle"></a>框架对象生命周期





框架对象的 "生命周期" 跨越从对象创建到删除对象的时间。 对象的引用计数将被删除。

### <a name="creating-a-framework-object"></a>创建框架对象

大多数框架对象是通过驱动程序对对象的创建方法的调用来创建的。 例如，每个 framework 驱动程序都必须调用 [**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate) 来创建框架驱动程序对象。

其他框架对象由框架创建。 例如，当用户应用程序打开设备进行读取或写入操作时，框架会创建一个框架文件对象并将其传递给驱动程序的 [*EvtDeviceFileCreate*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create) 回调函数。

框架或驱动程序可以创建几个框架对象。 例如，当 i/o 管理器向驱动程序提供 i/o 请求时，框架会创建一个框架请求对象并将其传递给驱动程序，这通常是通过调用某个驱动程序的请求处理程序来实现的。 驱动程序还可以创建框架请求对象并将其传递给其他驱动程序。

### <a name="using-reference-counts"></a>使用引用计数

框架维护每个对象的引用计数。 创建对象时，框架会将其引用计数设置为1。 如果引用计数变为零，则框架将删除该对象。

驱动程序可以通过调用 [**WdfObjectReference**](./wdfobjectreference.md) 以递增引用计数或 [**WdfObjectDereference**](./wdfobjectdereference.md) 来修改对象的引用计数，从而减少引用计数。  (仅当驱动程序之前调用 **WdfObjectReference** 时，才能调用 **WdfObjectDereference** 。 ) 

在大多数情况下，驱动程序不需要增加或减少对象的引用计数。 框架在将对象的句柄传递给驱动程序之前递增计数，并在驱动程序不再需要该对象时递减计数。

驱动程序调用 [**WdfObjectReference**](./wdfobjectreference.md) ，以确保在该驱动程序使用完对象之前，该对象不会 (框架或驱动程序线程) 删除。 有关驱动程序应调用 **WdfObjectReference** 和 [**WdfObjectDereference**](./wdfobjectdereference.md)的示例情况，请参阅 [同步取消已发送请求](synchronizing-cancellation-of-sent-requests.md)。

### <a name="deleting-a-framework-object"></a>删除框架对象

由于驱动程序调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) 或框架调用内部删除例程，因此将删除对象，但只有在对象的引用计数为零时，才会删除该对象。 当驱动程序或框架尝试删除某个对象之后，该对象的句柄保持有效，直到引用计数变为零。 驱动程序 *无法* 删除对象，只需调用 [**WdfObjectDereference**](./wdfobjectdereference.md) 将对象的引用计数递减到零，驱动程序也必须调用 **WdfObjectDelete**。

如果框架对象是父级的子对象，并且父对象正在被删除，则该框架将在删除父对象之前尝试删除该子对象。 对象的删除从最远离父对象的对象开始，并与根的对象层次结构建立在一起。

当驱动程序或框架删除对象时，驱动程序可以注册框架调用的以下两个回调函数：

-   一个 [*EvtCleanupCallback*](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup) 回调函数，框架将调用该函数，以便驱动程序可以调用 [**WdfObjectDereference**](./wdfobjectdereference.md) （如果它之前为正在删除的对象调用了 [**WdfObjectReference**](./wdfobjectreference.md) ）。

-   一个 [*EvtDestroyCallback*](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy) 回调函数，框架在对象的引用计数减少到零后调用该函数。

其中一个回调函数必须释放在创建对象时驱动程序所分配的任何特定于对象的资源。

框架始终处理删除某些框架对象，驱动程序不得尝试删除这些对象。 有关驱动程序无法删除的框架对象的列表，请参阅 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)。

 

