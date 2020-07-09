---
title: IRP_MJ_CLOSE （IFS）
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
ms.openlocfilehash: d9612df55783090503f4c31c2af94ef79798dfe3
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141324"
---
# <a name="irp_mj_close-ifs"></a>IRP \_ MJ \_ 关闭（IFS）


## <a name="when-sent"></a>发送时间


收到 IRP \_ MJ \_ 关闭请求表示文件对象上的引用计数已达到零，通常是因为文件系统驱动程序或其他内核模式组件在 file 对象上调用了[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject) 。 此请求通常遵循清理请求。 但是，这并不一定表示在清理请求后立即收到关闭请求。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


如果目标设备对象是文件系统的控制设备对象，则在执行任何所需的处理后，文件系统驱动程序必须完成 IRP。

否则，文件系统驱动程序应处理关闭请求。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


如果目标设备对象是筛选器驱动程序的控制设备对象，则筛选器驱动程序应执行与控制设备对象结束通信并完成 IRP 的必要操作。

否则，筛选器驱动程序应在执行任何所需的处理后将 IRP 向下传递到堆栈中的下一个较低的驱动程序，如删除筛选器驱动程序所维护的每个文件和每个文件对象上下文信息。

文件系统筛选器驱动程序编写器应注意到， [**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)导致[**IRP \_ MJ \_ 清理**](irp-mj-cleanup.md)请求被发送到卷的文件系统驱动程序堆栈。 由于文件系统通常会将流文件对象创建为[**IRP \_ MJ \_ create**](irp-mj-create.md)以外的操作的副作用，因此筛选器驱动程序很难可靠地检测流文件对象创建。 因此，筛选器驱动程序应该接收**irp \_ mj \_ 清除**和[**irp \_ mj \_ 关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)请求，以获取以前不可见的文件对象。

筛选器驱动程序编写器还应注意，与[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)不同， [**IoCreateStreamFileObjectLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)不会导致[**IRP \_ MJ \_ 清理**](irp-mj-cleanup.md)请求发送到文件系统驱动程序堆栈。 出于此原因，和由于文件系统通常会将流文件对象创建为[**IRP \_ MJ \_ create**](irp-mj-create.md)以外的操作的副作用，因此筛选器驱动程序很难可靠地检测流文件对象创建。 因此，筛选器驱动程序应该接收**IRP \_ MJ \_ 关闭**请求，才能获得以前不可见的文件对象。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。 （IRP 显示为*irp*。）驱动程序可以使用 IRP 的下列成员中设置的信息，并在处理关闭请求时使用 IRP 堆栈位置：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--flags"></a>*Irp- &gt; 标志*  
已为此请求设置以下标志：

IRP \_ 关闭 \_ 操作

IRP \_ 同步 \_ API

<a href="" id="irp--iostatus"></a>*Irp- &gt;IoStatus*指向[**IO \_ 状态 \_ 块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构的指针，该结构接收最终完成状态和有关请求的操作的信息。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt;* 指向与*DeviceObject*关联的文件对象的 FileObject 指针。

*IrpSp- &gt; FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件 \_ 对象结构。 文件对象结构的**RelatedFileObject**字段在 \_ 处理 IRP \_ MJ CLOSE 期间无效 \_ ，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt;MajorFunction*指定 IRP \_ MJ \_ CLOSE。

## <a name="see-also"></a>另请参阅


[**IO \_ 堆栈 \_ 位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)

[**IoCreateStreamFileObjectLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ 关闭（WDK 内核参考）**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)

[**IRP \_ MJ \_ 清除**](irp-mj-cleanup.md)

[**IRP \_ MJ \_ 创建**](irp-mj-create.md)

[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)

 

 






