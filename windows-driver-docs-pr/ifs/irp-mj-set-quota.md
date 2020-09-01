---
title: IRP_MJ_SET_QUOTA
description: IRP \_ MJ \_ 设置 \_ 配额
ms.assetid: 256c349b-48cb-4a9f-a60a-89503d8f3f58
keywords:
- IRP_MJ_SET_QUOTA 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_SET_QUOTA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70c60987c60ad09c6085f1bbe6584c5df08bfc3c
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066167"
---
# <a name="irp_mj_set_quota"></a>IRP \_ MJ \_ 设置 \_ 配额


## <a name="when-sent"></a>发送时间


IRP \_ MJ \_ 集 \_ 配额请求由 i/o 管理器发送。 例如，在用户模式应用程序调用了 Microsoft Win32 方法（如 **IDiskQuotaControl：： SetQuotaState**）的情况下，可以发送。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


\_ \_ \_ \_ 在 Windows NT 4.0 中存在 irp MJ 设置配额和 IRP mj \_ 查询配额， \_ 但文件系统未使用该配额。 在 Windows 2000 和更高版本的系统上，它们用于 NTFS 中的磁盘配额支持。 新文件系统支持这些 Irp 是可选的。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应将此 IRP 传递到堆栈上的下一个较低的驱动程序，除非它需要显式覆盖配额行为。

## <a name="parameters"></a>parameters


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用 irp 的下列成员中设置的信息，以及在处理集配额信息请求中的 irp 堆栈位置：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="deviceobject--flags"></a>*DeviceObject- &gt; 标志*  
如果设置了 "按 \_ 缓冲 \_ IO" 标记，则调用方请求方法 \_ 缓冲 i/o。 否则，调用方请求的方法 \_ 都不是 i/o。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp- &gt;AssociatedIrp.SystemBuffer*  
一个指针，指向系统提供的用于中间系统缓冲区的缓冲区（如果 \_ \_ 在 *DeviceObject &gt; 标志*中设置了 "执行缓冲 IO" 标记）。 否则，此成员设置为 **NULL**。

<a href="" id="irp--iostatus"></a>*Irp- &gt; IoStatus*  
指向 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的指针，该结构接收最终完成状态和有关请求的操作的信息。

<a href="" id="irp--userbuffer"></a>*Irp- &gt; UserBuffer*  
指向调用方提供的缓冲区的指针，该缓冲区包含要为卷添加或修改的配额条目。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*  
指向与 *DeviceObject*关联的文件对象的指针。

*IrpSp- &gt; FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件 \_ 对象结构。 文件对象结构的 **RelatedFileObject** 字段在 \_ 处理 IRP \_ MJ 集配额期间无效 \_ \_ ，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
指定 IRP \_ MJ \_ 设置 \_ 配额。

<a href="" id="irpsp--parameters-setquota-length"></a>*IrpSp- &gt; SetQuota. Length*  
指定 * &gt; UserBuffer*所指向的缓冲区的长度（以字节为单位）。

## <a name="see-also"></a>请参阅


[**文件 \_ 配额 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_quota_information)

[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCheckQuotaBufferValidity**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckquotabuffervalidity)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ 查询 \_ 配额**](irp-mj-query-quota.md)

 

