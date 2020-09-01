---
title: 创建框架请求对象
description: 创建框架请求对象
ms.assetid: 4bd668ec-14fb-4999-9535-a49712a26ba6
keywords:
- 请求对象 WDK KMDF，创建
- 请求对象 WDK KMDF，读取操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 482d85d1225bd4acdb459d1c4e4dc9d757ef2b1c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185857"
---
# <a name="creating-framework-request-objects"></a>创建框架请求对象





大多数框架请求对象由框架创建，但您的驱动程序还可以创建 request 对象。

### <a name="request-objects-created-by-the-framework"></a>由框架创建的请求对象

当基于框架的驱动程序从 i/o 管理器接收到 (IRP) 的 i/o 请求数据包时，框架会截获 IRP 并创建框架请求对象。 框架将请求对象置于 i/o 队列，如果驱动程序已为队列注册了 [请求处理](request-handlers.md) 程序，则将调用相应的处理程序。

下图说明了在框架为读取操作创建请求对象时发生的步骤。

![为读取操作创建请求对象的步骤](images/kmdf-creating-request-objects.png)

以下步骤与上图中的数字相对应：

1.  用户模式应用程序通过调用 Microsoft Win32 **ReadFile** 函数读取文件。

2.  **ReadFile**函数调用以内核模式运行的 i/o 管理器。

3.  I/o 管理器分配 IRP 结构，并将 [**irp \_ MJ \_ 读取**](../kernel/irp-mj-read.md) 函数代码存储在结构中。

4.  I/o 管理器将为驱动程序*x*调用[**DispatchRead**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)标准驱动程序例程，并向 IRP 结构传递指针。 由于驱动程序 *x* 是基于框架的驱动程序，因此框架提供驱动程序的 *DispatchRead* 例程。

5.  框架创建表示 IRP 结构的 request 对象。 框架将请求对象添加到驱动程序的某个队列对象。

6.  框架调用驱动程序的 [*EvtIoRead*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read) 请求处理程序，同时传递队列对象句柄和请求对象句柄。

### <a name="request-objects-created-by-a-driver"></a>请求驱动程序创建的对象

基于框架的驱动程序还可以创建请求对象。 例如，如果驱动程序收到的数据量大于驱动程序的 [i/o 目标](using-i-o-targets.md) 可以一次处理的数据量，则该驱动程序可能会创建请求对象。 在这种情况下，驱动程序可以将数据分成几个较小的请求，并使用其他请求对象将这些较小的请求发送到一个或多个 i/o 目标。

若要创建请求对象，驱动程序应调用 [**WdfRequestCreate**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate) ，然后调用初始化请求的框架对象方法（如 [**WdfUsbTargetPipeFormatRequestForRead**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread)）。

如果驱动程序通过使用框架来接收 WDM 调度例程中的 WDM Irp，然后服务或转发这些 Irp，则驱动程序可以调用 [**WdfRequestCreateFromIrp**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreatefromirp)。

 

