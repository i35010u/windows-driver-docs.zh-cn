---
title: 'IRP_MJ_CLEANUP (IFS) '
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
ms.openlocfilehash: 6ec04d7c374dce2c97ed99701c3f19adb7b84e33
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067410"
---
# <a name="irp_mj_cleanup-ifs"></a>\_ (IFS 的 IRP MJ \_ 清除) 


## <a name="when-sent"></a>发送时间


收到 IRP \_ MJ \_ 清除请求表示文件对象上的句柄引用计数已达到零。  (换言之，已关闭文件对象的所有句柄。 ) 通常在用户模式应用程序调用 Microsoft Win32 **CloseHandle** 函数时发送， (或者内核模式驱动程序已将最后一个未完成的句柄上的 [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)) 调用到文件对象。

需要注意的是，当某个文件对象的所有句柄都已关闭时，这并不一定表示该文件对象不再被使用。 诸如缓存管理器和内存管理器这样的系统组件可能会保留对文件对象的未处理引用。 即使在 \_ 收到 IRP MJ 清除请求之后，这些组件仍可以从文件读取或写入文件 \_ 。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


如果目标设备对象是文件系统的控制设备对象，则文件系统驱动程序必须完成 IRP。

否则，文件系统驱动程序应处理清理请求。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


如果目标设备对象是筛选器驱动程序的控制设备对象，则筛选器驱动程序必须完成 IRP。

否则，筛选器驱动程序应在执行任何所需的处理后将 IRP 向下传递到堆栈中的下一个较低的驱动程序。

文件系统筛选器驱动程序编写器应注意到， [**IoCreateStreamFileObject**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject) 导致 IRP \_ MJ \_ 清理请求被发送到卷的文件系统驱动程序堆栈。 由于文件系统通常会将流文件对象创建为 IRP MJ create 以外的操作的副作用 \_ \_ ，因此筛选器驱动程序很难可靠地检测流文件对象创建。 因此，筛选器驱动程序应该接收 IRP \_ mj \_ 清除和 irp \_ mj \_ 关闭请求，以获取以前不可见的文件对象。

筛选器驱动程序编写器还应注意，与 [**IoCreateStreamFileObject**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)不同， [**IoCreateStreamFileObjectLite**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite) 不会导致 IRP \_ MJ \_ 清理请求发送到文件系统驱动程序堆栈。 出于此原因，和由于文件系统通常会将流文件对象创建为 IRP MJ create 以外的操作的副作用 \_ \_ ，因此筛选器驱动程序很难可靠地检测流文件对象创建。 因此，筛选器驱动程序应该接收 IRP \_ MJ \_ 关闭请求，才能获得以前不可见的文件对象。

## <a name="parameters"></a>parameters


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用在进程清除请求中的以下 irp 成员和 irp 堆栈位置设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--flags"></a>*Irp- &gt; 标志*  
已为此请求设置以下标志：

IRP \_ 关闭 \_ 操作

IRP \_ 同步 \_ API

<a href="" id="irp--iostatus"></a>*Irp- &gt;IoStatus* 指向 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的指针，该结构接收最终完成状态和有关请求的操作的信息。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt;* 指向与*DeviceObject*关联的文件对象的 FileObject 指针。

*IrpSp- &gt; FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件 \_ 对象结构。 文件对象结构的 **RelatedFileObject** 字段在 \_ 处理 IRP \_ MJ 清除期间无效 \_ ，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt;MajorFunction* 指定 IRP \_ MJ \_ 清理。

## <a name="see-also"></a>另请参阅


[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCreateStreamFileObject**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)

[**IoCreateStreamFileObjectLite**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ 清理 (WDK 内核引用) **](../kernel/irp-mj-cleanup.md)

[**IRP \_ MJ \_ 关闭**](irp-mj-close.md)

[**IRP \_ MJ \_ 创建**](irp-mj-create.md)

[**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)

 

