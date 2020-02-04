---
title: IRP_MJ_CLOSE
description: IRP\_MJ\_CLOSE
ms.assetid: 62bb28de-7f89-4009-9ea9-0aa3d6bca0ed
keywords:
- IRP_MJ_CLOSE 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_CLOSE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20bf95ad79076b05173438981698a95951fe8045
ms.sourcegitcommit: c9fc8f401d13ea662709ad1f0cb41c810e7cb4c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/04/2020
ms.locfileid: "76977686"
---
# <a name="irp_mj_close"></a>IRP\_MJ\_CLOSE


## <a name="when-sent"></a>发送时间


收到 IRP\_MJ\_CLOSE 请求表示文件对象上的引用计数已达到零，通常是因为文件系统驱动程序或其他内核模式组件在 file 对象上调用了[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject) 。 此请求通常遵循清理请求。 但是，这并不一定表示在清理请求后立即收到关闭请求。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


如果目标设备对象是文件系统的控制设备对象，则在执行任何所需的处理后，文件系统驱动程序必须完成 IRP。

否则，文件系统驱动程序应处理关闭请求。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


如果目标设备对象是筛选器驱动程序的控制设备对象，则筛选器驱动程序应执行与控制设备对象结束通信并完成 IRP 的必要操作。

否则，筛选器驱动程序应在执行任何所需的处理后将 IRP 向下传递到堆栈中的下一个较低的驱动程序，如删除筛选器驱动程序所维护的每个文件和每个文件对象上下文信息。

文件系统筛选器驱动程序编写器应注意到， [**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)导致[**IRP\_MJ\_清理**](irp-mj-cleanup.md)请求发送到卷的文件系统驱动程序堆栈。 由于文件系统通常会将流文件对象创建为[**IRP\_MJ\_create**](irp-mj-create.md)以外的操作的副作用，因此筛选器驱动程序很难可靠地检测流文件对象创建。 因此，筛选器驱动程序应该接收**IRP\_mj\_清理**和[**irp\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)以前不可见的文件对象的请求。

筛选器驱动程序编写器还应注意，与[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)不同， [**IoCreateStreamFileObjectLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)不会导致[**IRP\_MJ\_清理**](irp-mj-cleanup.md)请求发送到文件系统驱动程序堆栈。 出于此原因，由于文件系统通常会将流文件对象创建为[**IRP\_MJ\_create**](irp-mj-create.md)以外的操作的副作用，因此筛选器驱动程序很难可靠地检测流文件对象创建。 因此，筛选器驱动程序应该接收**IRP\_MJ\_关闭**对之前不可见的文件对象的请求。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。 （IRP 显示为*irp*。）驱动程序可以使用 IRP 的下列成员中设置的信息，并在处理关闭请求时使用 IRP 堆栈位置：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--flags"></a>*Irp-&gt;标志*  
已为此请求设置以下标志：

IRP\_关闭\_操作

IRP\_同步\_API

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*指向[**IO\_状态的指针\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构，它接收最终完成状态和有关请求的操作的信息。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*指向与*DeviceObject*关联的文件对象的指针。

*&gt;IrpSp FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件\_对象结构。 文件\_对象结构的**RelatedFileObject**字段在处理 IRP\_MJ\_关闭期间无效，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*指定 IRP\_MJ\_CLOSE。

## <a name="see-also"></a>另请参阅


[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)

[**IoCreateStreamFileObjectLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_关闭（WDK 内核引用）** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)

[**IRP\_MJ\_清除**](irp-mj-cleanup.md)

[**IRP\_MJ\_创建**](irp-mj-create.md)

[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)

 

 






