---
title: IRP_MJ_SET_QUOTA
description: IRP\_MJ\_集\_配额
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
ms.openlocfilehash: 7b7ddca72cd120d6b698f39d558c9ebfabe7b4ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841147"
---
# <a name="irp_mj_set_quota"></a>IRP\_MJ\_集\_配额


## <a name="when-sent"></a>发送时间


IRP\_MJ\_集\_配额请求由 i/o 管理器发送。 例如，在用户模式应用程序调用了 Microsoft Win32 方法（如**IDiskQuotaControl：： SetQuotaState**）的情况下，可以发送。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


IRP\_MJ\_设置\_配额和 IRP\_MJ\_查询\_配额存在于 Windows NT 4.0 中，但未被文件系统使用。 在 Windows 2000 和更高版本的系统上，它们用于 NTFS 中的磁盘配额支持。 新文件系统支持这些 Irp 是可选的。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应将此 IRP 传递到堆栈上的下一个较低的驱动程序，除非它需要显式覆盖配额行为。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。 （IRP 显示为*irp*。）驱动程序可以使用 IRP 的下列成员中设置的信息，以及在处理集配额信息请求中的 IRP 堆栈位置：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="deviceobject--flags"></a>*DeviceObject-&gt;标志*  
如果设置了 DO\_缓冲\_IO 标志，则调用方请求\_缓冲 i/o 的方法。 否则，调用方请求的方法不\_i/o。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp. SystemBuffer*  
指向系统提供的要用作中间系统缓冲区的缓冲区的指针（如果\_缓冲\_IO 标志是在*DeviceObject-&gt;标记*中设置的。 否则，此成员设置为**NULL**。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[**IO\_状态的指针\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构，它接收最终完成状态和有关请求的操作的信息。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
指向调用方提供的缓冲区的指针，该缓冲区包含要为卷添加或修改的配额条目。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
指向与*DeviceObject*关联的文件对象的指针。

*&gt;IrpSp FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件\_对象结构。 文件\_对象结构的**RelatedFileObject**字段在处理 IRP\_MJ\_设置\_配额时无效，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_集\_配额。

<a href="" id="irpsp--parameters-setquota-length"></a>*IrpSp-&gt;参数. SetQuota. 长度*  
指定由*Irp&gt;* 的缓冲区的长度（以字节为单位）。

## <a name="see-also"></a>另请参阅


[**文件\_配额\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_quota_information)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCheckQuotaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckquotabuffervalidity)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_QUERY\_配额**](irp-mj-query-quota.md)

 

 






