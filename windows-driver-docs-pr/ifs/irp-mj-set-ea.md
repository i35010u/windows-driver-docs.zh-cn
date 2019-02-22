---
title: IRP_MJ_SET_EA
description: IRP\_MJ\_SET\_EA
ms.assetid: f9e1f867-a473-46ac-a1c0-63534c4c0755
keywords:
- IRP_MJ_SET_EA 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_SET_EA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd2716e9a9b385f4f9772c3c4972e394669c6eb6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554261"
---
# <a name="irpmjsetea"></a>IRP\_MJ\_SET\_EA


## <a name="when-sent"></a>发送时间


I/O 管理器发送 IRP\_MJ\_设置\_EA 请求文件中设置的扩展属性。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


如果文件系统支持扩展的属性，文件系统驱动程序应处理该请求，并完成 IRP。 否则，文件系统驱动程序应返回**状态\_EAS\_不\_支持**。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应在堆栈上传递此 IRP 到下一步低驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和在处理组扩展的属性请求的 IRP 堆栈位置中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
指向包含要设置的扩展的属性信息的系统提供的输入缓冲区的指针。 用于方法\_缓冲 I/O。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)接收最终完成状态以及有关请求的操作信息的结构。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  
内存描述符列表 (MDL) 描述接收的扩展的属性信息的输入的缓冲区的地址。 用于方法\_直接 I/O。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
指向调用方提供[**文件\_完整\_EA\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545793)-接收的扩展的属性信息的结构化输入的缓冲区。 用于方法\_既不 I/O。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
与之关联的文件对象的指针*DeviceObject*。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的 IRP 处理期间\_MJ\_设置\_EA 和不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_设置\_EA。

<a href="" id="irpsp--parameters-setea-length"></a>*IrpSp-&gt;Parameters.SetEa.Length*  
以字节为单位的输入缓冲区的长度。

## <a name="see-also"></a>另请参阅


[**文件\_完整\_EA\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff545793)

[**IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoCheckEaBufferValidity**](https://msdn.microsoft.com/library/windows/hardware/ff548252)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_查询\_EA**](irp-mj-query-ea.md)

 

 






