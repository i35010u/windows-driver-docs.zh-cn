---
title: IRP_MJ_CLEANUP
description: IRP\_MJ\_CLEANUP
ms.assetid: e4593d99-a721-4ab1-82a5-b32b9c312b25
keywords:
- IRP_MJ_CLEANUP 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_CLEANUP
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a67023be7034846d67cbe78055e5910f281f2b8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841182"
---
# <a name="irp_mj_cleanup"></a>IRP\_MJ\_CLEANUP


## <a name="when-sent"></a>发送时间


收到 IRP\_MJ\_清除请求时，表示文件对象上的句柄引用计数已达到零。 （换言之，已关闭文件对象的所有句柄。）通常，在用户模式应用程序将最后一个未完成的句柄上的 Microsoft Win32 **CloseHandle**函数（或一个内核模式驱动程序调用[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)）调用到文件对象时，会发送该函数。

需要注意的是，当某个文件对象的所有句柄都已关闭时，这并不一定表示该文件对象不再被使用。 诸如缓存管理器和内存管理器这样的系统组件可能会保留对文件对象的未处理引用。 即使在收到 IRP\_MJ\_清除请求之后，这些组件仍可以从文件读取或写入文件。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


如果目标设备对象是文件系统的控制设备对象，则文件系统驱动程序必须完成 IRP。

否则，文件系统驱动程序应处理清理请求。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


如果目标设备对象是筛选器驱动程序的控制设备对象，则筛选器驱动程序必须完成 IRP。

否则，筛选器驱动程序应在执行任何所需的处理后将 IRP 向下传递到堆栈中的下一个较低的驱动程序。

文件系统筛选器驱动程序编写器应注意到， [**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)导致 IRP\_MJ\_清理请求发送到卷的文件系统驱动程序堆栈。 由于文件系统通常会将流文件对象创建为 IRP\_MJ\_CREATE 以外的操作的副作用，因此筛选器驱动程序很难可靠地检测流文件对象创建。 因此，筛选器驱动程序应该接收 IRP\_MJ\_清理和 IRP\_MJ\_关闭以前不可见的文件对象的请求。

筛选器驱动程序编写器还应注意，与[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)不同， [**IoCreateStreamFileObjectLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)不会导致 IRP\_MJ\_清理请求发送到文件系统驱动程序堆栈。 出于此原因，由于文件系统通常会将流文件对象创建为 IRP\_MJ\_CREATE 以外的操作的副作用，因此筛选器驱动程序很难可靠地检测流文件对象创建。 因此，筛选器驱动程序应该接收 IRP\_MJ\_关闭对之前不可见的文件对象的请求。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。 （IRP 显示为*irp*。）驱动程序可以使用 IRP 的下列成员中设置的信息，并使用 IRP 堆栈位置来处理清除请求：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--flags"></a>*Irp-&gt;标志*  
已为此请求设置以下标志：

IRP\_关闭\_操作

IRP\_同步\_API

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*指向[**IO\_状态的指针\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构，它接收最终完成状态和有关请求的操作的信息。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*指向与*DeviceObject*关联的文件对象的指针。

*&gt;IrpSp FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件\_对象结构。 文件\_对象结构的**RelatedFileObject**字段在处理 IRP\_MJ\_清除期间无效，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*指定 IRP\_MJ\_清除。

## <a name="see-also"></a>另请参阅


[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)

[**IoCreateStreamFileObjectLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_清除（WDK 内核引用）** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)

[**IRP\_MJ\_关闭**](irp-mj-close.md)

[**IRP\_MJ\_创建**](irp-mj-create.md)

[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)

 

 






