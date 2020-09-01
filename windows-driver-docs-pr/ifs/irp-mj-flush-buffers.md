---
title: 'IRP_MJ_FLUSH_BUFFERS (IFS) '
description: IRP \_ MJ \_ 刷新 \_ 缓冲区
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
ms.openlocfilehash: 4b56e93f4f28cc31c03675409769dd88e3ca21fc
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067400"
---
# <a name="irp_mj_flush_buffers-ifs"></a>IRP \_ MJ \_ 刷新 \_ 缓冲区 (IFS) 


## <a name="when-sent"></a>发送时间


\_ \_ \_ 当缓冲数据需要刷新到磁盘时，由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送 IRP MJ 刷新缓冲区请求。 例如，在用户模式应用程序调用 Microsoft Win32 函数（如 **FlushFileBuffers**）时，可以将其发送。  (文件系统驱动程序和文件系统筛选器驱动程序，调用 [**CcFlushCache**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ccflushcache) 通常比发送 IRP 更好。 ) 

维护数据的内部缓冲区的所有文件系统和筛选器驱动程序都必须处理此 IRP，以便可以在系统关闭范围内保留对文件数据或元数据的更改。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应将与文件对象关联的任何重要数据或元数据刷新到磁盘，并完成 IRP。 有关如何处理此 IRP 的详细信息，请学习 FASTFAT 示例。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应刷新与文件对象关联的任何重要数据或元数据，并将此 IRP 向下传递到堆栈上的下一个较低版本的驱动程序。

## <a name="parameters"></a>parameters


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用在处理刷新缓冲区请求中的以下 irp 成员和 irp 堆栈位置设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--iostatus"></a>*Irp- &gt; IoStatus*  
指向 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的指针，该结构接收最终完成状态和有关请求的操作的信息。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*  
指向与 *DeviceObject*关联的文件对象的指针。

*IrpSp- &gt; FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件 \_ 对象结构。 文件对象结构的 **RelatedFileObject** 字段在 \_ 处理 IRP \_ MJ 刷新缓冲区期间无效 \_ \_ ，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
指定 IRP \_ MJ \_ 刷新 \_ 缓冲区。

## <a name="see-also"></a>请参阅


[**CcFlushCache**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ccflushcache)

[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ 刷新 \_ 缓冲区 (WDK 内核参考) **](../kernel/irp-mj-flush-buffers.md)

 

