---
title: IRP_MJ_SET_QUOTA
description: IRP\_MJ\_SET\_QUOTA
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
ms.openlocfilehash: 8cecd00a300cee4e85c4d1ef5f19cf886c554741
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533770"
---
# <a name="irpmjsetquota"></a>IRP\_MJ\_SET\_QUOTA


## <a name="when-sent"></a>发送时间


IRP\_MJ\_设置\_配额请求发送的 I/O 管理器。 它可以发送，例如，在用户模式应用程序具有如调用 Microsoft Win32 方法时**IDiskQuotaControl::SetQuotaState**。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


IRP\_MJ\_设置\_配额和 IRP\_MJ\_查询\_配额 Windows NT 4.0 中存在但未由文件系统。 在 Windows 2000 和更高版本的系统，它们用于在 NTFS 磁盘配额支持。 对这些 Irp 通过新的文件系统的支持是可选的。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应在堆栈上传递此 IRP 到下一步低驱动程序，除非它需要显式重写配额行为。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和在处理组配额信息请求的 IRP 堆栈位置中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象指针。

<a href="" id="deviceobject--flags"></a>*DeviceObject-&gt;标志*  
如果执行操作\_缓冲\_IO 标志设置，调用方已请求方法\_缓冲 I/O。 否则，调用方已请求方法\_既不 I/O。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
指向要用作中间系统缓冲区，如果系统提供缓冲区的指针是否\_缓冲\_中设置了 IO 标志*DeviceObject-&gt;标志*。 否则，此成员设置为**NULL**。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)接收最终完成状态以及有关请求的操作信息的结构。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
指向包含要添加或修改的卷的配额项的调用方提供的缓冲区的指针。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
与之关联的文件对象的指针*DeviceObject*。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的 IRP 处理期间\_MJ\_设置\_配额并不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_设置\_配额。

<a href="" id="irpsp--parameters-setquota-length"></a>*IrpSp-&gt;Parameters.SetQuota.Length*  
指定的长度，以字节为单位通过指向的缓冲区*Irp-&gt;UserBuffer*。

## <a name="see-also"></a>另请参阅


[**文件\_配额\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540342)

[**IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoCheckQuotaBufferValidity**](https://msdn.microsoft.com/library/windows/hardware/ff548279)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_查询\_配额**](irp-mj-query-quota.md)

 

 






