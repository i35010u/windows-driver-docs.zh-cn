---
title: 创建框架请求对象
description: 创建框架请求对象
ms.assetid: 4bd668ec-14fb-4999-9535-a49712a26ba6
keywords:
- 请求对象 WDK KMDF，创建
- 请求对象 WDK KMDF 读取操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04371c4af8287355560a00f666fb525f2330c356
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524391"
---
# <a name="creating-framework-request-objects"></a>创建框架请求对象





大多数 framework 请求对象创建的框架，但您的驱动程序也可以创建请求对象。

### <a name="request-objects-created-by-the-framework"></a>由框架创建的请求对象

时基于 framework 的驱动程序从 I/O 管理器接收的 I/O 请求数据包 (IRP)，框架将截获 IRP，并创建一个框架请求对象。 框架将请求对象放入 I/O 队列和驱动程序已注册[请求处理程序](request-handlers.md)队列，请调用相应的处理程序。

下图演示了框架创建用于读取操作的请求对象时发生的步骤。

![若要创建的读取操作的请求对象的步骤](images/kmdf-creating-request-objects.png)

以下步骤对应于在上图中的数字：

1.  在用户模式应用程序读取的文件时，通过调用 Microsoft Win32 **ReadFile**函数。

2.  **ReadFile**函数调用 I/O 管理器，它在内核模式下运行。

3.  I/O 管理器分配的 IRP 结构，并将存储[ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794)函数在结构中的代码。

4.  I/O 管理器调用[ **DispatchRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)驱动程序的标准驱动程序例程*x*，指针传递给 IRP 结构。 因为驱动程序*x*是基于 framework 的驱动程序，该框架提供的驱动程序*DispatchRead*例程。

5.  框架将创建一个表示 IRP 结构的请求对象。 该框架将请求对象添加到驱动程序的队列对象之一。

6.  框架将调用的驱动程序[ *EvtIoRead* ](https://msdn.microsoft.com/library/windows/hardware/ff541776)请求处理程序，并传递队列对象句柄和请求对象句柄。

### <a name="request-objects-created-by-a-driver"></a>创建一个驱动程序的请求对象

基于框架的驱动程序还可以创建请求对象。 例如，驱动程序可能会创建请求对象，如果它收到读取或写入请求大于在驱动程序的数据量[I/O 目标](using-i-o-targets.md)可以处理一次。 在这种情况下，该驱动程序可以将数据划分为多个较小请求，并使用额外的请求对象将这些较小的请求发送到一个或多个 I/O 目标。

若要创建一个请求对象，您的驱动程序应调用[ **WdfRequestCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff549951) framework 对象方法，如初始化请求后, 跟[ **WdfUsbTargetPipeFormatRequestForRead**](https://msdn.microsoft.com/library/windows/hardware/ff551136)。

如果驱动程序 WDM 的调度例程中接收 WDM Irp，然后服务或将其转发使用框架，该驱动程序可以调用[ **WdfRequestCreateFromIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549953)。

 

 





