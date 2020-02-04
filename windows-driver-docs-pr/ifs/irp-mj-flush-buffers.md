---
title: IRP_MJ_FLUSH_BUFFERS
description: IRP\_MJ\_刷新\_缓冲区
ms.assetid: 13df0d84-0320-4d7e-9acc-8f913ba6afaa
keywords:
- IRP_MJ_FLUSH_BUFFERS 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_FLUSH_BUFFERS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0d27d227cd3567c553d78cc552bf547b7dcc8ef
ms.sourcegitcommit: c9fc8f401d13ea662709ad1f0cb41c810e7cb4c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/04/2020
ms.locfileid: "76977678"
---
# <a name="irp_mj_flush_buffers"></a>IRP\_MJ\_刷新\_缓冲区


## <a name="when-sent"></a>发送时间


当缓冲数据需要刷新到磁盘时，由 i/o 管理器和其他操作系统组件以及其他的内核模式驱动程序发送 IRP\_MJ\_刷新\_缓冲区请求。 例如，在用户模式应用程序调用 Microsoft Win32 函数（如**FlushFileBuffers**）时，可以将其发送。 （对于文件系统驱动程序和文件系统筛选器驱动程序，调用[**CcFlushCache**](https://msdn.microsoft.com/library/windows/hardware/ff539082)通常比发送 IRP 更好。）

维护数据的内部缓冲区的所有文件系统和筛选器驱动程序都必须处理此 IRP，以便可以在系统关闭范围内保留对文件数据或元数据的更改。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应将与文件对象关联的任何重要数据或元数据刷新到磁盘，并完成 IRP。 有关如何处理此 IRP 的详细信息，请学习 FASTFAT 示例。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应刷新与文件对象关联的任何重要数据或元数据，并将此 IRP 向下传递到堆栈上的下一个较低版本的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。 （IRP 显示为*irp*。）驱动程序可以使用 IRP 的下列成员中设置的信息，并使用 IRP 堆栈位置来处理刷新缓冲区请求：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[**IO\_状态的指针\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构，它接收最终完成状态和有关请求的操作的信息。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
指向与*DeviceObject*关联的文件对象的指针。

*&gt;IrpSp FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件\_对象结构。 文件\_对象结构的**RelatedFileObject**字段在处理 IRP\_MJ\_刷新\_缓冲区期间无效，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_刷新\_缓冲区。

## <a name="see-also"></a>另请参阅


[**CcFlushCache**](https://msdn.microsoft.com/library/windows/hardware/ff539082)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_刷新\_缓冲区（WDK 内核引用）** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)

 

 






